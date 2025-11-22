.. _index:

.. title:: PocketMine-MP

.. figure:: https://raw.githubusercontent.com/pmmp/PocketMine-MP/stable/.github/readme/pocketmine-rgb.gif
   :figclass: light-only
   :align: center

.. figure:: https://raw.githubusercontent.com/pmmp/PocketMine-MP/stable/.github/readme/pocketmine-dark-rgb.gif
   :figclass: dark-only
   :align: center

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

PocketMine-MP is a highly customisable server software for Minecraft: Bedrock Edition, built from scratch in PHP, with over 10 years of history.

If you're looking to create a Minecraft: Bedrock server with **custom functionality**, look no further.

- 🧩 **Powerful plugin API** - extend and customise gameplay as you see fit
- 🗺️ **Rich ecosystem** and **large developer community** - find plugins easily and learn to develop your own
- 🌐 **Multi-world support** - offer a more varied game experience to players without transferring them to other server nodes
- 🏎️ **Performance** - get 100+ players onto one server (depending on hardware and plugins)
- ⤴️ **Continuously updated** - new Minecraft versions are usually supported within days

.. note::
   
   **PocketMine-MP is NOT a vanilla Minecraft server software.**
   It is poorly suited to hosting vanilla survival servers.
   It doesn't have many features from the vanilla game, such as vanilla world generation, redstone, mob AI, and various other things.

   If you just want to play **vanilla survival multiplayer**, consider using the `official Minecraft: Bedrock server software <https://minecraft.net/download/server/bedrock>`_ instead of PocketMine-MP.

   If that's not an option for you, you may be able to add some of PocketMine-MP's missing features using plugins from `Poggit <https://poggit.pmmp.io/plugins>`_, or write plugins to implement them yourself.

.. toctree::
    :maxdepth: 1
    :caption: Getting Started

    installation
    basic-usage
    connecting
    configuration
    plugins
    worlds
    resourcepacks
    permissions
    contributing
    issues
    contact

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
    :caption: Developer Resources
    :maxdepth: 1

    developers/plugin-docs-index.rst
    developers/*
