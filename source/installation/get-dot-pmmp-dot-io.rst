.. _get_pmmp_io:

Using the official installer (Linux/MacOS only)
-----------------------------------------------

.. warning::
    Only works on Linux or MacOS.

If you're creating a new server, create a directory which you want to install PocketMine-MP into, and ``cd`` into it.

Otherwise, just ``cd`` straight into your existing server folder.

Installing/updating to the latest version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Then use ``curl`` to install/update PocketMine-MP using the following command:

.. code-block:: sh

    curl -sL https://get.pmmp.io | bash -s -

or, if you don't have ``curl``, try ``wget``:

.. code-block:: sh

    wget -q -O - https://get.pmmp.io | bash -s -

.. code-block:: log

  [*] Retrieving latest build data for channel "stable"
  [*] Found PocketMine-MP 5.2.0 (build 2166) for Minecraft: PE v1.20.0 (PHP 8.1)
  [*] This stable build was released on Tue 01 Jul 2023 02:00:00 PM UTC
  [-] This channel should have a signature, none found
  [*] Installing/updating PocketMine-MP on directory ./
  [1/3] Cleaning...
  [2/3] Downloading PocketMine-MP phar... done!
  [3/3] Obtaining PHP: detecting if build is available... Linux PHP build available... downloading 8.1 ... updating php.ini... checking... done
  [*] Everything done! Run ./start.sh to start PocketMine-MP



.. error::

    It is recommended to run it as a **normal user** as it doesn't need further permissions.

    **Do not run the installer as root, this is discouraged**.
	
.. note::

    If the installer doesn't work for you, try :ref:`installing manually <installing-manually>`.

Installing a specific version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you don't want to run the latest version, you may be able to run an older version by giving the ``-v`` option to the installer.

Examples:

+-------------------+--------------------------------------------------------+
| Version           | Command                                                |
+===================+========================================================+
| Latest 4.x stable | ``curl -sL https://get.pmmp.io | bash -s - -v 4``      |
+-------------------+--------------------------------------------------------+
| Latest 5.x beta   | ``curl -sL https://get.pmmp.io | bash -s - -v 5-beta`` |
+-------------------+--------------------------------------------------------+
| Latest 5.1 stable | ``curl -sL https://get.pmmp.io | bash -s - -v 5.1``    |
+-------------------+--------------------------------------------------------+

You can see a list of available options for ``-v`` by clicking `here <https://github.com/pmmp/update.pmmp.io/tree/master/channels>`_.
