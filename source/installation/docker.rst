.. _docker:

Using Docker (Linux only)
~~~~~~~~~~~~~~~~~~~~~~~~~
Docker is an easy, safe way to run software in a container where it can't affect anything else on your machine.
You don't need to build any dependencies, and updating is as simple as changing the version number of the image you're using.

Pre-requisites
--------------

To install Docker, refer to the `official Docker docs <https://docs.docker.com/engine/install/>`_.

Running the server
------------------

This is really easy once you have ``docker`` installed.

.. code-block:: sh

   mkdir wherever-you-want
   cd wherever-you-want
   mkdir data plugins
   sudo chown -R 1000:1000 data plugins
   docker run -it -p 19132:19132/udp -v $PWD/data:/data -v $PWD/plugins:/plugins ghcr.io/pmmp/pocketmine-mp


To run a specific version, just add it to the end of the command, like this:

.. code-block:: sh

   docker run -it -p 19132:19132/udp -v $PWD/data:/data -v $PWD/plugins:/plugins ghcr.io/pmmp/pocketmine-mp:4.0.0

This command will run version ``4.0.0`` of PocketMine-MP instead of the latest version.

Run the server in the background
================================

To start the server in the background, change ``-it`` to ``-itd`` in the ``docker run`` command. (No need to ``screen``/``tmux`` anymore!)

Alternatively, you can press ``Ctrl p`` ``Ctrl q`` to exit the server console and leave the server running.

Opening the console of a server running in the background
=========================================================

Use ``docker ps`` to see a list of running containers. It will look like this:

.. code-block:: sh

   user@DYLANS-PC:~/pm-docker-test$ docker ps
   CONTAINER ID   IMAGE                      COMMAND                  CREATED         STATUS         PORTS                                                                              NAMES
   dc20edd3dd62   pmmp/pocketmine-mp:4.0.0   "start-pocketmine"       7 seconds ago   Up 6 seconds   19132/tcp, 0.0.0.0:19132-19133->19132-19133/udp, :::19132-19133->19132-19133/udp   brave_dijkstra

In this case, the container name is ``brave_dijkstra``, but it might be something else in your case.
You can also use the container ID instead of the name.

To open the console, run the following command:

.. code-block:: sh

   docker attach <container name or ID>

To leave the console, just press ``Ctrl p`` ``Ctrl q``.

Viewing the logs (without opening the console)
==============================================

To see the logs, run the following command:

.. code-block:: sh

   docker logs --tail=100 <container name you saw in docker ps>

Change ``--tail=100`` to the number of recent lines in the log you want to see.

Managing the server
-------------------

Changing the server port
========================

Docker allows you to map ports, so you don't need to edit ``server.properties``.

In the run command shown above, change ``19132:19132/udp`` to ``<port number you want>:19132/udp``. **Note: Do not change the second number.**

.. warning::
   Do not change the port in ``server.properties``. This is unnecessary when using Docker and will make things more complicated.

Managing the server data
========================

The server's data is stored in Docker volumes.

In the ``docker run`` command, you'll normally bind these volumes to local folders where you want the container to store its data.
For example, the ``-v $PWD/data:/data`` argument of the ``docker run`` command above maps the ``/data`` folder inside the container to the ``./data`` folder wherever you ran the command.

You can change the location of the folder used by changing the path before the ``:``. For example, ``-v /home/dktapps/pocketmine_data:/data`` will make the container store its files in
``/home/dktapps/pocketmine_data``.

+--------------+------------+-----------------------------------------------------------------------------+
| Volume       | Type       | Description                                                                 |
+==============+============+=============================================================================+
| ``/data``    | Read-write | ``server.properties``, ``pocketmine.yml``, player data, worlds, plugin data |
+--------------+------------+-----------------------------------------------------------------------------+
| ``/plugins`` | Read-only  | Plugin code (e.g. ``.phar`` files)                                          |
+--------------+------------+-----------------------------------------------------------------------------+

.. warning::
   If you add new files (e.g. a world) to these folders manually, don't forget to change the ownership of the file/folder to ``1000:1000``:

   ``sudo chown -R 1000:1000 <file/folder you added>``

   This is needed to make the server able to access the file/folder.

Adding plugins from Poggit
==========================

If the ``POCKETMINE_PLUGINS`` environment variable is set, the container will auto-download the plugins specified from https://poggit.pmmp.io
before starting PocketMine-MP.

The list of plugins should be given in the format ``PluginOne:1.2.3 PluginTwo:4.5.6``. The version part (``:4.5.6``) is optional.

.. caution::

   Plugins won't be redownloaded if they're already in the `plugins` volume, even if the version is different.
   If you need to update a plugin, you'll need to delete the old plugin `.phar` first.

Advanced usage: Passing args to ``PocketMine-MP.phar`` inside the container
---------------------------------------------------------------------------
The ``POCKETMINE_ARGS`` environment variable will be passed to ``PocketMine-MP.phar`` when run.


