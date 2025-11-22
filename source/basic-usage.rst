
Basic usage
~~~~~~~~~~~

Starting the server
-------------------

- Linux/MacOS: run ``./start.sh``
- Windows: Double-click ``start.cmd``, or open PowerShell in the server directory and run ``.\start.ps1``.

Setup Wizard
------------

The first time PocketMine-MP starts, it launches a setup wizard.

The setup wizard will allow you to choose a language, and guide you through setting up basic information about your new server, like its name, the server port, etc.

.. note::

    You'll be asked to accept the terms of PocketMine-MP's license.
    You can read the full text of the license on `GitHub <https://github.com/pmmp/PocketMine-MP/blob/master/LICENSE>`_.

.. tip::

    You can skip the setup wizard by passing ``--no-wizard`` to ``start.sh``, ``start.cmd`` or ``start.ps1``.


Stopping the server
-------------------

To stop the server, simply type ``stop`` in the console and press enter.

.. error::

    Do NOT click the X to stop the server. You could lose data or your data might get corrupted.

Running the server in the background (Linux/MacOS only)
-------------------------------------------------------

If you're using a VPS to host PocketMine-MP, you'll probably want to be able to run the server in the background so that you can keep using your shell, and also be able to get back into the server console later on when reconnecting to the host.

For this purpose, we recommend using the ``screen`` command. You can usually install it using your OS's package manager (e.g. ``apt``) if you don't have it installed.

Starting a screen for a new server instance
===========================================

To create a new screen, ``cd`` into the server folder and run the following:

.. code-block:: sh

   screen -S pocketmine

.. tip::

   You can change ``pocketmine`` to anything you want. This is just an identifier for the screen so you can get back to it later.

   If you want to run multiple PocketMine-MP instances, you'll want to start multiple screens and give each one a different identifier.

Once inside the screen, you can run ``./start.sh`` as normal.

Putting the server in the background
====================================

To get out of the screen and put the server in the background, press ``Ctrl a`` ``Ctrl d``. You'll see a message like this:

.. code-block:: sh

   [detached from 395586.pocketmine]

Opening the console of a server running in the background
=========================================================

To get back to the console of a server you've already started:

.. code-block:: sh

   screen -r pocketmine

Replace ``pocketmine`` with the name you gave to the ``-S`` flag when creating the screen.

.. tip::

   This command may not work if your SSH connection was interrupted, or if another user is viewing the screen in another shell.

   If you need to forcibly take control of the screen, try using ``screen -D -RR <screen name>`` instead.

Listing active screens
======================

If you can't remember the name of your screen and/or have multiple screens (e.g. with multiple running servers):

.. code-block:: sh

   screen -ls

This will output something like:

.. code-block:: sh

   There is a screen on:
        395586.pocketmine       (11/22/25 19:13:05)     (Detached)
   1 Socket in /run/screen/S-user.

In this example, we would be able to reconnect to the screen using ``screen -r 395586.pocketmine`` or ``screen -r pocketmine``.

Closing the screen after stopping the server
============================================

You can close the screen by typing ``exit`` inside it, the same as you would for a normal shell.
