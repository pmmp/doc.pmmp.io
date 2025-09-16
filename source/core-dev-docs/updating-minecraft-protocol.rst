.. _updating_pocketmine_minecraft:

Implementing new Minecraft version support in PocketMine-MP
-----------------------------------------------------------

Minecraft often makes changes to its network protocol, including adding new packets, removing old ones, or changing the structure of existing packets.
Because of this, PocketMine-MP often needs to be updated to support the latest version of Minecraft.

This page will cover the basic process of analyzing and implementing protocol updates.

Pre-requisites
~~~~~~~~~~~~~~

- Linux (WSL2 will work)
- Linux version of `Bedrock Dedicated Server <https://www.minecraft.net/en-us/download/server/bedrock>`_ compatible with your target version of Minecraft
- Minecraft world with the desired features to test (optionally with experiments enabled, e.g. 1.21 Update)
- Git clones of `PocketMine-MP <https://github.com/pmmp/PocketMine-MP>`_, `BedrockProtocol <https://github.com/pmmp/BedrockProtocol>`_, `BedrockData <https://github.com/pmmp/BedrockData>`_, `BedrockBlockUpgradeSchema <https://github.com/pmmp/BedrockBlockUpgradeSchema>`_, and `BedrockItemUpgradeSchema <https://github.com/pmmp/BedrockItemUpgradeSchema>`_
- A local copy of `BedrockProtocolDumper <https://github.com/pmmp/BedrockProtocolDumper>`_

Step 1: Generating supporting data (part 1)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PocketMine-MP requires additional data from the new version of Minecraft to function correctly. This includes:

These data originate from several sources:

1. `protocol_info_dumper.py <https://github.com/pmmp/bds-modding-devkit/blob/master/protocol_info_dumper.py>`_ which generates basic version info and packet ID lists for updating BedrockProtocol.
2. Mods of the Bedrock Dedicated Server that dump the needed data. This method is a pain, but it's the only way to get some data.
3. Packet traces of the Bedrock Dedicated Server communicating with a vanilla Minecraft client.

Tools to collect all of this data are provided in `bds-modding-devkit <https://github.com/pmmp/bds-modding-devkit>`_.

Follow the instructions in the `modding toolkit`_ repository README to set up the modding environment and install the BDS version you want to dump data from.

.. note::

        Unfortunately, Mojang no longer publicly provide BDS builds with debugging symbols as of 1.21.40. **This means that you need access to BDS builds provided by a server or Marketplace partner to generate the needed data.**

        Some of the data can be scraped from the public protocol docs instead, but not all data can be collected from the docs either. This leaves third party servers dependent on the goodwill of Minecraft partners.

Generating basic protocol info from BDS
.......................................

Use the `protocol info dumper <https://github.com/pmmp/bds-modding-devkit/blob/master/protocol_info_dumper.py>`_ to generate ``protocol_info.json`` for ``BedrockData``.

This script requires Python 3, ``objdump`` (install the ``binutils`` package), and a BDS binary with debugging symbols.

Use it like so: ``python3 protocol_info_dumper.py ./bedrock_server_symbols.debug ./protocol_info.json``

Once you have the file, put it in your ``BedrockData`` folder.

Getting data from BDS via mods
..............................


The mod code of interest can be found in the `data extraction mod`_ main repository.
This mod is preinstalled by the modding toolkit when you clone following the instructions in the README.

Once you've generated the data, copy all the files (not the folders) in ``mapping_files/`` to ``BedrockData``.

There may be additional files that are not needed by ``BedrockData``. You can ignore these.

.. note::

	The code often needs to be updated to work with the latest version of the BDS.
	This guide won't cover how to make the mods run on newest BDS, as the changes needed are usually different from version to version, and this guide would end up very long.
	You really should have general experience modding BDS before trying to get into this.
	If you need help, ask in the PMMP Discord server.

.. warning::

	Make sure the ``input_files/old_block_palettes`` submodule is up to date, and that it contains a block palette for the previous version of Minecraft.
	You'll need this later for generating blockstate upgrade schemas.

Collecting vanilla <-> vanilla packet traces
............................................

The `modding toolkit`_ also provides a `tracer script`_ that can be used to hook into a running instance of BDS and capture packet traces between a vanilla client and server.
This script uses the `Frida.re <https://frida.re>`_ Python API to hook into packet read and write functions in the BDS.
The script has no impact on vanilla behaviour, guaranteeing the best quality data.

These traces can be used to generate data, and also to verify that your changes to `BedrockProtocol`_ are correct.

Steps to capture packet traces:

1. Create a new world in Minecraft on the target version. Make sure to enable any experiments which add new blocks or items, as these need to be present for generating data upgrade schemas.
2. Configure ``server.properties`` on your BDS to use the world you generated.
3. Start ``bedrock_server_symbols.debug`` directly (do not use ``start.sh``).
4. In a separate terminal, run the following command: ``sudo python3 tracer.py rw bedrock_server_symbols.debug``. This will hook into the running BDS instance and start capturing packet traces.
5. Join the BDS server using Minecraft. Do whatever in-game tests you need to get the game to send packets you want to see.
6. Stop the server. The script will print the filename of the trace file it generated. This usually looks something like ``packets_123456789.txt``.

This trace file will be used later on to generate further data, but it's necessary to update BedrockProtocol before doing so.

.. warning::
	Do not use ``tracer.py`` on a server with mods loaded. The BDS instance may crash or behave unexpectedly.

.. note::

	You may have difficulty joining a BDS server running inside WSL2 from a Windows Minecraft client. This is a long-standing issue between WSL2 and UWP apps and has no known fix.
	You can work around it by using a basic proxy script like `RakLib proxy.php <https://github.com/pmmp/RakLib/blob/stable/tools/proxy.php>`_ and joining via the proxy instead of trying to connect directly.
	Alternatively, just run the server on a proper Linux machine or VM.

.. note::

	If you don't want to use ``tracer.py``, you can also create a packet trace using a proxy such as `gophertunnel`_.
	The structure of the file is simple: each line is starts with ``read:`` or ``write:`` followed by the packet buffer encoded as base64.
	However, a proxy may change the structure, order and timings of packets, so it may not give the same quality of data as the tracer script.

Step 2: Update code in BedrockProtocol and PocketMine-MP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``BedrockProtocol`` is where most of the manual work needs to be done.

1. Use ``tools/update-from-bedrock-data.php`` in ``BedrockProtocol`` to generate the basics from the data you generated for step 1. This will update a few enums and add stub classes for new packets. **Files will not be removed for deleted packets.**

2. Analyze what changes need to be made to packet structures. This typically involves one or more of the following methods:

  - Reading the official `Minecraft Bedrock protocol documentation <https://github.com/Mojang/bedrock-protocol-docs>`_ - these are the easiest to use, but sometimes miss changes or are incorrect
  - Using tools like `IDA`_ to decompile ``bedrock_server_symbols.debug`` and analyze packet source code (you need the x86_64 decompiler to work on BDS)

3. Update packet structures and information in ``BedrockProtocol``. This includes:

  - Writing code to encode and decode new packets
  - Adjusting structures of existing packets and their subtypes if necessary
  - Updating constants and/or enums to match the new version
  - Whether new packet(s) should be clientbound, serverbound, or both

4. Run ``tools/generate-create-static-methods.php`` in ``BedrockProtocol``. This will update the ``::create()`` methods for all packets to match the new packet structures. (Make sure to run ``php-cs-fixer`` afterwards. It won't break anything if you don't, but the script will mess up the formatting.)
5. Do any necessary changes to PocketMine-MP to make it compatible with the updated ``BedrockProtocol``. You can run PHPStan to find out where changes need to be made.

.. note::

	You can link locally-modified versions of ``BedrockProtocol`` and related repositories to PocketMine-MP. This makes it easier to do integration testing without having to commit anything.

	Use the provided `script <https://github.com/pmmp/PocketMine-MP/blob/stable/install-local-protocol.sh>`_ to link your local copies of ``BedrockProtocol``, ``BedrockBlockUpgradeSchema``, ``BedrockItemUpgradeSchema``, and ``BedrockData`` to ``PocketMine-MP``.

.. note::

	If you suspect that the official protocol documentation is incorrect, you can use tools like `IDA`_ to decompile the BDS binary and analyze the packet code directly.
	However, this can be a very frustrating and time-consuming process, as `IDA`_ is very slow and laggy when working with large binaries like BDS.

	You can also use ``gdb`` to look at BDS's compiled assembly code, which can be much faster, but is also much more difficult to understand.

Step 3: Generating supporting data (part 2)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generating the remaining files for BedrockData
..............................................

Now that you've updated ``BedrockProtocol``, use tools in ``PocketMine-MP`` to generate data from the packet trace you collected in part 1.

.. note::

        ``BedrockProtocol`` code must be updated to handle the new version's packets before trying to parse packet traces.

Use PocketMine-MP's ``tools/generate-bedrock-data-from-packets.php`` to parse the packet trace ``.txt`` file you collected earlier, like so:

.. code-block:: sh

        cd pocketmine-mp
        php tools/generate-bedrock-data-from-packets.php ./packets_123456789.txt ../deps/BedrockData

This will extract various information from the packet dump, like creative inventory items, crafting recipes, and more.
Once you've done this, ``BedrockData`` is ready to publish. However, do not push anything to the master branch until the official Mojang release day.

Generating a blockstate upgrade schema
......................................

PocketMine-MP uses JSON schemas to tell it how to upgrade blockstate NBT data in old world saves to the newest version.

Steps to generate a blockstate upgrade schema:

1. Get the appropriate palette mapping file that the BDS mod generated. You can find it in ``mapping_files/old_palette_mappings``, and the file name will be something like ``1.20.80.24_beta_to_current_block_map.bin``.
2. Use PocketMine-MP's ``tools/generate-blockstate-upgrade-schema.php`` to generate a new schema for this version.
3. Add the schema to the ``nbt_upgrade_schema`` folder of ``BedrockBlockUpgradeSchema``. The name should be prefixed with a number to ensure the files are sorted correctly, like this: ``0271_1.20.70.24_beta_to_1.20.80.24_beta.json``.
4. Commit the new schema. **Do not commit directly to the master branch until the version is released.**

.. note::

	If you can't get a palette mapping file, you can write an upgrade schema by hand.
	However, this may be time-consuming and error-prone, and is not recommended unless you have no other choice.

Generating an item upgrade schema
.................................

PocketMine-MP uses JSON schemas to upgrade item data in old world saves to the newest version.

Steps to generate an item upgrade schema:

1. Use PocketMine-MP's ``tools/generate-item-upgrade-schema.php``. Give it the path to ``r16_to_current_item_map.json`` in ``BedrockData``, and the path to the already-existing schemas in ``BedrockItemUpgradeSchema``.
2. Add the schema to the ``id_meta_upgrade_schema`` folder of ``BedrockItemUpgradeSchema``. The name should be prefixed with a number to ensure the files are sorted correctly, like this: ``0181_1.20.70.24_beta_to_1.20.80.24_beta.json``.
3. Commit the new schema. **Do not commit directly to the master branch until the version is released.**

Step 4: Completing changes in PocketMine-MP using the new data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you have finished generated supporting data, you may need to do a few more changes to PocketMine-MP.

This mostly involves updating the code in ``src/data/bedrock/block`` and ``src/data/bedrock/item`` to decode and encode data in the expected format for the newest version.

If you're lucky, the version you're updating to might not have changed anything at all. In this case, you won't need to do anything.

Steps to do the changes:

1. Run ``composer update-codegen``.
2. Run ``vendor/bin/phpstan``. This will tell you where you need to make changes.
3. Fix all the problems reported by PHPStan.
4. Make sure the following constants are updated correctly:

	- ``BlockStateData::CURRENT_VERSION`` (often changes)
	- ``BedrockWorldData::CURRENT_STORAGE_VERSION`` (rarely changes)
	- ``BedrockWorldData::CURRENT_STORAGE_NETWORK_VERSION`` (always changes)
	- ``BedrockWorldData::CURRENT_CLIENT_VERSION_TARGET`` (always changes)
	- ``LevelDB::CURRENT_LEVEL_CHUNK_VERSION`` (rarely changes)
	- ``LevelDB::CURRENT_LEVEL_SUBCHUNK_VERSION`` (rarely changes)

5. Run ``vendor/bin/phpunit tests/phpunit``. Make sure all the tests pass. If you've made a mistake somewhere, the tests should fail.

Step 5: Playtesting PocketMine-MP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you've made all the changes, you should playtest PocketMine-MP to make sure everything works as expected.

1. Create a new world with Minecraft on the target version.
2. Load the world into PocketMine-MP and start the server.
3. Do whatever playtests you need to make sure your changes work as expected.

Finally: Committing the results
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you're happy with your changes, commit the changes on all repositories.
By convention, we recommend you name your branch like this: ``bedrock-1.21.0``.

When the new version's final release is out, merge the changes into the main branches and tag releases where appropriate.

.. note::

	The ``Bedrock*`` repositories use tag metadata (suffixed using a ``+`` sign) to show which version of Minecraft they support.
	An example tag looks something like this: ``1.9.0+bedrock-1.20.80``.

	The metadata doesn't affect dependency version resolution, but it can be useful for telling at a glance which version the repository supports.

.. _modding toolkit: https://github.com/pmmp/bds-modding-devkit
.. _data extraction mod: https://github.com/pmmp/bds-mod-mapping
.. _tracer script: https://github.com/pmmp/bds-modding-devkit/blob/master/tracer.py
.. _IDA: https://hex-rays.com/
.. _gophertunnel: https://github.com/Sandertv/gophertunnel
