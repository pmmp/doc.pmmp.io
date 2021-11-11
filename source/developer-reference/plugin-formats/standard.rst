.. _standard_plugin_formats:

Standard plugin types
~~~~~~~~~~~~~~~~~~~~~

Phar
----

This plugin format consists of a single `PHAR <https://www.php.net/manual/en/intro.phar.php>`_ file which bundles all of the files necessary to make the plugin work.
This type of plugin is commonly used to distribute pre-made plugins, because they are easy for users to download and move around without needing to modify the plugin code.

Loading
=======

1. Drop the ``.phar`` file into your ``plugins`` directory.
2. Restart the server. The plugin will be loaded (if compatible).

