.. _plugin_yml_spec_optional_fields:

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

.. note::
    While it is possible to nest permission declarations in PocketMine-MP versions prior to 4.0.0, it's recommended *not* to do this because it causes unfixable bugs in permission defaults. (In effect, nested permissions are just a very weird and confusing way to declare permission groups.)
    Instead, you should give your permissions consistent names so that permission plugins can pattern-match them.
