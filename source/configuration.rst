.. _configuration:

Configuration
=============

Server behaviour
----------------

PocketMine-MP's behaviour is controlled by several configuration files. You can edit them to change the behaviour of your server.

* ``server.properties`` contains basic settings like the server name, port, maximum view distance, etc. These settings are all safe to change.
* ``pocketmine.yml`` contains more advanced settings settings like memory usage, max thread count, etc. It also contains settings for loading multiple worlds.

.. warning::

    It's best to **leave a setting alone** if you don't understand what it's for. Many settings in ``pocketmine.yml`` can break your server if configured incorrectly.

.. note::

    To edit configs on Windows, right-click on the file → Open With → Choose another app → Notepad.


Resource packs
--------------

``resource_packs.yml`` is found in the ``resource_packs`` folder.

:ref:`Read more about installing resource packs. <resourcepacks>`


Player permissions
------------------

There are several files that allow you to control player permissions on your server:

* ``ops.txt`` is a simple list of player names that have "op" permissions on your server. Ops can do more things than regular players, like giving items, teleporting, stopping the server and more.
* ``banned-players.txt`` lists names of players that are banned from your server.
* ``banned-ips.txt`` lists IPs that are not allowed to connect to your server. This is useful for troublesome players who change accounts and keep coming back to hassle you.

.. note::

    You can modify these by using slash commands instead of editing the files directly.
    See ``/op``, ``/deop``, ``/ban``, ``/unban``, ``/ban-ip`` and ``/unban-ip``.
