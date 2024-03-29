.. _plugin_yml_spec:

``plugin.yml`` fields
+++++++++++++++++++++

``plugin.yml`` is a manifest file which contains information about a plugin.

.. contents:: Contents
   :depth: 3
   :local:

Required fields
~~~~~~~~~~~~~~~

name
----

Type: ``string``

Name of the plugin. This may contain letters, numbers, hyphens, periods and underscores. It may also contain spaces, but this is discouraged.

version
-------

Type: ``string``

Self explanatory. It's recommended to use a 3-point semantic version, but this can be anything you like.

main
----

Type: ``string``

Fully-qualified name of the main class. This class must meet the following criteria:

- MUST NOT be abstract
- MUST implement the ``pocketmine\plugin\Plugin`` interface

api
---

Type: ``string`` or ``string[]``

The API version(s) that the plugin is compatible with. If the plugin's API version is not compatible with that of the server, the server will refuse to load the plugin. More info on API versioning can be found `here <api_version_spec>`.

Optional fields
~~~~~~~~~~~~~~~

Cosmetic
--------

website
=======

Type: ``string``

Website for the plugin.

description
===========

Type: ``string``

Short description of the plugin.

prefix
======

Type: ``string``

Alternative prefix to use in the plugin's log messages. Defaults to the plugin name.

author
======

Type: ``string``

Author name of the plugin.

authors
=======

Type: ``string[]``

A list of author names, if there are more than one. If both ``author`` and ``authors`` are defined, a list will be formed containing both.

Plugin loading controls
-----------------------

load
====

Type: ``string``

When in the startup sequence to prefer loading this plugin. Currently can be one of ``STARTUP`` or ``POSTWORLD``. See plugin load order. (TODO: add a link here)

depend
======

Type: ``string`` or ``string[]``

List of plugins that this plugin depends on. Plugin will not load if any of these plugins are missing.

softdepend
==========

Type: ``string`` or ``string[]``

List of plugins that the plugin can **optionally** depend on. Plugins in this list must load prior to the plugin soft-depending on them.

loadbefore
==========

Type: ``string`` or ``string[]``

List of plugins that this plugin must load prior to. Works like a soft-dependency in reverse.

extensions
==========

Type: ``array``

List of PHP extensions that the plugin requires. Plugin will not load if any are missing or have unmet version constraints.
TODO: examples

mcpe-protocol
=============

Type: ``int`` or ``int[]``

List of Minecraft PE network protocol versions the plugin is compatible with. Plugin will fail to load if the current server protocol version is not in this list.

os
==

.. versionadded:: 3.12.0

Type: ``string`` or ``string[]``

List of operating systems that the plugin will run on. If not present, the plugin will load on any OS.
Possible values include ``win``, ``mac``, ``linux``, ``android``, ``ios``, ``bsd``.

Misc
----

commands
========

Type: ``array``

Definitions of commands implemented by this plugin in the ``onCommand()`` of the ``PluginBase``.

Example:

.. code-block:: yaml

    commands:
      # The name of the command the user will type to execute it
      example:
        # Description that will be shown in help command
        description: Example command
        # Shown to the user if they type the command in incorrectly
        usage: "/example"
        aliases:
          - ex
          - examp
        # Permission required to run the command
        permission: exampleperm.command.example
        # Shown to the user if they don't have permission to run the command
        permission-message: "You do not have permission to use this example command!"


permissions
===========

Type: ``array``

List of permissions defined by this plugin, usually used for commands.

Example:

.. code-block:: yaml

    permissions:
      exampleperm.command.example:
        description: "Allows the user to run the example command"
        # Default state of the permission. Explanation of each value:
        # op: only op players have this permission by default
        # true: everyone has this permission by default
        # false: no one has this permission by default
        default: true

src-namespace-prefix
====================

.. versionadded:: 4.0.0

Type: ``string``

Base namespace of the classes in your ``src/`` folder. Defaults to empty string.

This allows you to have a longer namespace for your classes without having to create useless nested folders in your plugin structure.

Examples:

+-----------------------------------+-------------------------------------------------+---------------------------------------------------------+
| Value of ``src-namespace-prefix`` | Name of class including namespace               | Path class will be loaded from                          |
+===================================+=================================================+=========================================================+
| (empty)                           | ``YourName\PluginName\Main``                    | ``src/YourName/PluginName/Main.php``                    |
|                                   +-------------------------------------------------+---------------------------------------------------------+
|                                   | ``YourName\PluginName\SubNamespace\OtherClass`` | ``src/YourName/PluginName/SubNamespace/OtherClass.php`` |
+-----------------------------------+-------------------------------------------------+---------------------------------------------------------+
| ``YourName\PluginName``           | ``YourName\PluginName\Main``                    | ``src/Main.php``                                        |
|                                   +-------------------------------------------------+---------------------------------------------------------+
|                                   | ``YourName\PluginName\SubNamespace\OtherClass`` | ``src/SubNamespace/OtherClass.php``                     |
+-----------------------------------+-------------------------------------------------+---------------------------------------------------------+
