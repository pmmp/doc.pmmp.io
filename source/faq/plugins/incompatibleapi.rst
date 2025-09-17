What does "Incompatible API version" mean when loading a plugin?
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

This means that the version of the plugin currently installed is not compatible with the server. This might be because your version of PocketMine-MP is out of date, or because the plugin itself is out of date.

Why does it matter what version I'm using?
------------------------------------------

New features are added to the API over time, and old ones may be deprecated.
In addition, in a major version bump (e.g. 4.x -> 5.x), there may be **backwards-incompatible changes** (sometimes referred to as *BC breaks*) which prevent plugins working on different major versions.

Plugins declare which API versions they support to make sure their plugins fail gracefully instead of crashing your server or making it do something unexpected.

.. tip::

   You can learn more about how API versions work :ref:`here <api_version_spec>`.

What can I do?
--------------
Check for an updated version of the plugin, or ask the plugin developer to update it.

If you're feeling adventurous, you could try updating the code yourself to work on the version of PocketMine-MP you're using. Check out the :ref:`plugin development docs <plugin_docs_index>`. Also, consider joining our `Discord <https://discord.gg/bge7dYQ>`_ server so that you can ask other developers for help.

.. warning::
	Simply bumping the plugin's declared API version is often not enough to update a plugin. The plugin might still crash or not work as expected.
	Use of so-called "API updaters" is discouraged.
