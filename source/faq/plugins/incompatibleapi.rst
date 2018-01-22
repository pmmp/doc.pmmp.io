What does "Incompatible API version" mean when loading a plugin?
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

This means that the version of the plugin currently installed is not compatible with the server. Check for an updated version of the plugin, ask the plugin developer to update it, or try updating it yourself.

PocketMine-MP's API frequently undergoes breaking and substantial changes. The API version exists as a way for a plugin and server to determine whether the plugin can work correctly on the server's current API.

.. warning::
	Simply bumping the plugin's declared API version is often not enough to update a plugin. The plugin might still crash or not work as expected.
	Use of so-called "API updaters" is discouraged.
