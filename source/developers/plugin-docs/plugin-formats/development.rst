.. _development_plugin_formats:

Development plugin types
~~~~~~~~~~~~~~~~~~~~~~~~

Since the standard types of plugins are usually pretty difficult to work with while developing a plugin, there are more types of plugins that developers can use, but these are **not** recommended for distribution.

Folder
------

**Note:** this plugin format is **not** enabled by default. The `DevTools`_ plugin is required to load this type of plugin.

This plugin format is similar to a PHAR plugin in structure, but all the files are in a folder on the disk instead of inside a phar file.
This gives you easy access to the source code when you're developing a plugin.

This plugin format is commonly used for development, because it is just as feature-complete as a PHAR plugin, and can be compiled to a PHAR plugin when you're ready to release it.

You can see the `ExamplePlugin <https://github.com/pmmp/ExamplePlugin>`_ or any plugin source-code repository to get an idea of how this should look.

Loading
=======

1. If you don't have the `DevTools`_ plugin, `download its phar file <https://github.com/pmmp/DevTools/releases/latest>`_ and put it in your ``plugins`` folder.
2. Move the folder containing the plugin's source code into your ``plugins`` folder. The plugin's folder should contain a ``plugin.yml`` file and a ``src`` folder.
3. Restart the server and the plugin will be loaded.


Script
------

A script plugin is a single ``.php`` file. They're useful for quickly testing features without creating a full plugin structure.

There are some key differences between a script plugin and other types of plugins:

- Instead of a ``plugin.yml``, the basic metadata of the plugin is declared in a PHPDoc comment at the top of the file
- You can declare multiple classes, but all of them must be inside the script plugin's ``.php`` file
- Resources and ``config.yml`` files are not supported by default
- ``onCommand()`` is not supported
- Any manifest attribute that accepts arrays or objects (e.g. ``commands``, ``permissions``, ``authors``) is not supported

Check out the `example on GitHub <https://github.com/pmmp/PocketMine-MP/blob/stable/examples/plugins/ExampleScriptPlugin.php>`_.

Loading
=======

1. Drop the ``.php`` file into your ``plugins`` folder.
2. Restart the server and the plugin will be loaded.

.. _DevTools: https://github.com/pmmp/DevTools/releases
