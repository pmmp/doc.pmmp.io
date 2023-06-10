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

.. code-block:: sh

  [*] Found PocketMine-MP Final_1.5dev (build 1254) using API 1.12.0
  [*] This development build was released on Sat Jun 20 09:45:04 CEST 2015
  [*] Installing/updating PocketMine-MP on directory ./
  [1/3] Cleaning...
  [2/3] Downloading PocketMine-MP Final_1.5dev-1254 phar... done!
  [3/3] Obtaining PHP: detecting if build is available...
  [3/3] MacOS 64-bit PHP build available, downloading PHP_5.6.10_x86-64_MacOS.tar.gz... checking... regenerating php.ini... done
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
