.. _index:

.. title:: PocketMine-MP

.. image:: img/PocketMine-MP.png
   :align: center

|

.. raw:: html

   <p align="center">
	<a href="https://github.com/pmmp/PocketMine-MP/actions/workflows/main.yml"><img src="https://github.com/pmmp/PocketMine-MP/workflows/CI/badge.svg" alt="CI" /></a>
	<a href="https://github.com/pmmp/PocketMine-MP/releases/latest"><img alt="GitHub release (latest SemVer)" src="https://img.shields.io/github/v/release/pmmp/PocketMine-MP?label=release&sort=semver"></a>
	<a href="https://hub.docker.com/r/pmmp/pocketmine-mp"><img src="https://img.shields.io/docker/v/pmmp/pocketmine-mp?logo=docker&label=image" alt="Docker image version (latest semver)" /></a>
	<a href="https://discord.gg/bge7dYQ"><img src="https://img.shields.io/discord/373199722573201408?label=discord&color=7289DA&logo=discord" alt="Discord" /></a>
	<br>
	<a href="https://github.com/pmmp/PocketMine-MP/releases"><img alt="GitHub all releases" src="https://img.shields.io/github/downloads/pmmp/PocketMine-MP/total?label=downloads%40total"></a>
	<a href="https://github.com/pmmp/PocketMine-MP/releases/latest"><img alt="GitHub release (latest by SemVer)" src="https://img.shields.io/github/downloads/pmmp/PocketMine-MP/latest/total?sort=semver"></a>
   </p>

.. rst-class:: center

    `Plugin Repository <https://poggit.pmmp.io/plugins>`_ • `Forums <https://forums.pmmp.io>`_ • `Discord <https://discord.gg/bge7dYQ>`_ • `Source Code <https://github.com/pmmp>`_

PocketMine-MP is a custom server software for the Minecraft: Bedrock family of Minecraft editions (includes Android, iOS, W10 and others).

What features does it have?
===========================
- A powerful plugin API, which allows you to extend and customize your server far more easily and extensively than any competing server implementations, including the official vanilla server.
- Multi-world support, allowing you to offer a more varied game experience to players without transferring them to other server nodes.
- Performance fit to hold 100+ players (depends on hardware, see the :ref:`requirements` section).
- Continuously updated to support latest Minecraft versions. PocketMine-MP has the longest and best track record of any custom server for compatibility with new Minecraft versions.

.. note::

   PocketMine-MP is **NOT** a complete vanilla server, and it doesn't have some features you would find in the vanilla game.

   If you just want to play *survival multiplayer* and don't care about *plugins*, you should consider using the `official Minecraft: Bedrock server software <https://minecraft.net/download/server/bedrock>`_ instead of using PocketMine-MP.

.. toctree::
    :maxdepth: 1
    :caption: Getting Started

    installation
    basic-usage
    configuration
    plugins
    resourcepacks
    contact
    links

.. toctree::
    :caption: Frequently Asked Questions & Common Issues
    :maxdepth: 1
    :glob:

    faq/installation
    faq/connecting
    faq/playing
    faq/plugins
    faq/about

.. toctree::
    :glob:
    :maxdepth: 1
    :caption: Issues, Bugs and Crashes

    issues/*

.. toctree::
    :caption: Plugin Developer Resources
    :maxdepth: 1

    developer-resources
