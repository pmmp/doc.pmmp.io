.. _installation:

Installation
============

Using https://get.pmmp.io (Linux/MacOS only)
--------------------------------------------
.. warning::
    Only works on Linux or MacOS.

Create a directory which you want to install PocketMine-MP into, and ``cd`` into it.

Then use ``curl`` or ``wget`` to install PocketMine-MP using the following command:

.. code-block:: sh

    curl -sL https://get.pmmp.io | bash -s -
    wget -q -O - https://get.pmmp.io | bash -s -

.. code-block:: sh

  [*] Found PocketMine-MP Final_1.5dev (build 1254) using API 1.12.0
  [*] This development build was released on Sat Jun 20 09:45:04 CEST 2015
  [*] Installing/updating PocketMine-MP on directory ./
  [1/3] Cleaning...
  [2/3] Downloading PocketMine-MP Final_1.5dev-1254 phar... done!
  [3/3] Obtaining PHP: detecting if build is available...
  [3/3] MacOS 64-bit PHP build available, downloading PHP_5.6.10_x86-64_MacOS.tar.gz... checking... regenerating php.ini... done
  [*] Everything done! Run ./start.sh to start PocketMine-MP

.. error::

    It is recommended to run it as a **normal user** as it doesn't need further permissions.

    **Do not run the installer as root, this is discouraged**.



Installing manually
-------------------

No installer available for your platform? Did the installer fail? It is not your taste? YOLO? DIY!

Getting PHP for your server
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Download your flavor PHP binary (`downloads`_)
2. Extract the PHP binary into your server directory. If everything went well, you should have a `bin` folder in your server directory.
3. (Windows only) Download and install Microsoft Visual C++ Redistributable 2017 (`downloads`_)

Getting PocketMine-MP
~~~~~~~~~~~~~~~~~~~~~

Using .phar
***********

1. Create a new directory for PocketMine-MP.
2. Download PocketMine-MP.phar (`downloads`_)
3. Rename the .phar to ``PocketMine-MP.phar``.
4. Place it in the PocketMine-MP directory you just created.
5. Get the start script for your platform (`Windows CMD <https://github.com/pmmp/PocketMine-MP/blob/master/start.cmd>`_, `Windows PowerShell <https://github.com/pmmp/PocketMine-MP/blob/master/start.ps1>`_, `Linux/MacOS bash <https://github.com/pmmp/PocketMine-MP/blob/master/start.sh>`_)
6. (Linux/MacOS only) Make start.sh executable (chmod +x start.sh)

Using Git
*********

You can also run PocketMine-MP from source code by cloning the GitHub repository using Git.

.. code::

    git clone https://github.com/pmmp/pocketmine-mp.git --recursive

.. warning::
    Remember to clone with the ``--recursive`` flag! PocketMine-MP has several submodules which are required to run the server.

    If you forgot the ``--recursive`` flag when you cloned, you can cd into the server directory and run ``git submodule update --init --recursive``.

Starting for the first time
---------------------------
- Linux/MacOS: run ``./start.sh``
- Windows: Double-click ``start.cmd``, or open PowerShell in the server directory and run ``.\start.ps1``.

The first time PocketMine-MP starts, it launches a set-up wizard. This can be disabled by running ``./start.sh --no-wizard``.

.. code::

    $ ./start.sh
    [*] PocketMine-MP set-up wizard
    [*] Please select a language:
    English => en
    EspaÃ±ol => es
    ä¸­æ–‡ => zh
    PyccÄ¸Ð¸Ð¹ => ru
    æ—¥æœ¬èªž => ja
    Deutsch => de
    í•œêµ­ì–´ => ko
    Nederlands => nl
    FranÃ§ais => fr
    Italiano => it
    Melayu => ms
    Norsk => no
    Svenska => sv
    Suomi => fi
    TÃ¼rkÃ§e => tr
    [?] Language (en):

PocketMine-MP supports a few other languages.
Fill in the two letters behind the language and press enter.
Is your language not in the list? Add it on `Crowdin`_.

.. code::

    [*] English has been correctly selected.
    Welcome to PocketMine-MP!
    Before starting setting up your new server you have to accept the license.
    PocketMine-MP is licensed under the LGPL License,
    that you can read opening the LICENSE file on this folder.

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU Lesser General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    [?] Do you accept the License? (y/N):

Do you accept the `License`_?

.. code::

    [?] Do you want to skip the set-up wizard? (y/N):

You can skip the wizard from here and start the server with the default settings or continue.

.. code::

    [*] You are going to set up your server now.
    [*] If you don't want to change the default value, just press Enter.
    [*] You can edit them later on the server.properties file.
    [?] Give a name to your server (Minecraft: PE Server):
    [*] Do not change the default port value if this is your first server.
    [?] Server port (19132):
    [*] Choose between Creative (1) or Survival (0)
    [?] Default Game mode (0):
    [?] Max. online players (20):
    [*] The spawn protection disallows placing/breaking blocks in the spawn zone except for OPs
    [?] Enable spawn protection? (Y/n):
    [*] An OP is the player admin of the server. OPs can run more commands than normal players
    [?] OP player name (example, your game name):
    [!] You will be able to add an OP user later using /op <player>
    [*] The white-list only allows players in it to join.
    [?] Do you want to enable the white-list? (y/N):
    [!] Query is a protocol used by different tools to get information of your server and players logged in.
    [!] If you disable it, you won't be able to use server lists.
    [?] Do you want to disable Query? (y/N):
    [*] RCON is a protocol to remote connect with the server console using a password.
    [?] Do you want to enable RCON? (y/N):
    [*] Getting your external IP and internal IP
    [!] Your external IP is [your external IP]. You may have to port-forward to your internal IP [your internal IP]
    [!] Be sure to check it, if you have to forward and you skip that, no external players will be able to join. [Press Enter]

    [*] You have finished the set-up wizard correctly
    [*] Check the Plugin Repository to add new features, minigames, or advanced protection to your server
    [*] PocketMine-MP will now start. Type /help to view the list of available commands.

    [10:18:38] [Server thread/INFO]: Loading pocketmine.yml...
    [10:18:38] [Server thread/INFO]: Loading server properties...
    [10:18:38] [Server thread/INFO]: Selected English (eng) as the base language
    [10:18:38] [Server thread/INFO]: Starting Minecraft: PE server version v1.1.0.55
    [10:18:38] [Server thread/INFO]: Opening server on 0.0.0.0:19132
    [10:18:38] [Server thread/INFO]: This server is running PocketMine-MP version 1.7dev "[REDACTED]" (API 3.0.0-ALPHA7)
    [10:18:38] [Server thread/INFO]: PocketMine-MP is distributed under the LGPL License
    [10:18:38] [Server thread/INFO]: Loading recipes...
    [10:18:38] [Server thread/INFO]: Loading resource packs...
    [10:18:39] [Server thread/NOTICE]: Level "world" not found
    [10:18:39] [Server thread/INFO]: Preparing level "world"
    [10:18:39] [Server thread/NOTICE]: Spawn terrain for level "world" is being generated in the background
    [10:18:39] [Server thread/INFO]: Starting GS4 status listener
    [10:18:39] [Server thread/INFO]: Setting query port to 19132
    [10:18:39] [Server thread/INFO]: Query running on 0.0.0.0:19132
    [10:18:39] [Server thread/INFO]: Default game type: Survival Mode
    [10:18:39] [Server thread/INFO]: Done (59.006s)! For help, type "help" or "?"

The server should have started now and you should be able to join.

.. _downloads: links.html#downloads
.. _GitHub: https://github.com/pmmp/pocketmine-mp/releases
.. _Crowdin: http://translate.pocketmine.net
.. _License: https://github.com/pmmp/pocketmine-mp/blob/master/LICENSE
