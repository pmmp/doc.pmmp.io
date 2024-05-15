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

Basic changes to BedrockProtocol and PocketMine-MP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``BedrockProtocol`` is where most of the manual work needs to be done.

1. Use ``protocol_info_generator_objdump.py`` in ``BedrockProtocolDumper`` to generate packet ID lists and version information. This script requires Python 2, and takes a path to a ``bedrock_server_symbols.debug`` file and a path to your ``BedrockProtocol`` local copy. The following things will be updated:

  - ``src/PacketPool.php``
  - ``src/ProtocolInfo.php``
  - ``src/PacketHandler.php``
  - ``src/PacketHandlerInterface.php``
  - New files may be added if there are new packets in the version you are updating to. However, files will **not** be removed for deleted packets - that's up to you to do manually.

2. Analyze what changes need to be made to packet structures. This typically involves one or more of the following methods:

  - Reading the official `Minecraft Bedrock protocol documentation <https://github.com/Mojang/bedrock-protocol-docs>`_ - these are the easiest to use, but sometimes miss changes or are incorrect
  - Using tools like `IDA <https://hex-rays.com/>`_ to decompile ``bedrock_server_symbols.debug`` and analyze packet source code (you need the x86_64 decompiler to work on BDS)

3. Update packet structures and information in ``BedrockProtocol``. This includes:

  - Writing code to encode and decode new packets
  - Adjusting structures of existing packets and their subtypes if necessary
  - Updating constants and/or enums to match the new version

4. Run ``tools/generate-create-static-methods.php`` in ``BedrockProtocol``. This will update the ``::create()`` methods for all packets to match the new packet structures. (Make sure to run ``php-cs-fixer`` afterwards. It won't break anything if you don't, but the script will mess up the formatting.)
5. Link your updated local copy of ``BedrockProtocol`` to your PocketMine-MP server. PocketMine-MP provides a `script <https://github.com/pmmp/PocketMine-MP/blob/stable/install-local-protocol.sh>`_ for doing this easily without having to commit any changes or release dependencies.
6. Do any necessary changes to PocketMine-MP to make it compatible with the updated ``BedrockProtocol``. You can run PHPStan to find out where changes need to be made.

Generating supporting data
~~~~~~~~~~~~~~~~~~~~~~~~~~

PocketMine-MP requires additional data from the new version of Minecraft to function correctly. This includes:

- Schemas for upgrading saved block NBT to the latest version (``BedrockBlockUpgradeSchema``)
- Schemas for upgrading saved item IDs to the latest version (``BedrockItemUpgradeSchema``)
- Internal block, item, biome, entity, creative and crafting data (``BedrockData``)

These data originate from two sources:

1. Mods of the Bedrock Dedicated Server that dump the needed data. This method is a pain, but it's the only way to get some data. This could become a problem in the future if Mojang proceed with their plans to remove debugging symbols from the BDS.
2. Packet traces of the Bedrock Dedicated Server communicating with a vanilla Minecraft client. These can be obtained in several different ways, but not all required data can be obtained this way.

[to be continued]
