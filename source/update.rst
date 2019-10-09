.. _update:

Updating
========

.. contents::
    :local:
    :depth: 2

Update using the installer (Linux/MacOS only)
---------------------------------------------
You can also use the installer on these platforms to update your installation. Passing the ``-u`` flag will update the PocketMine-MP installation.

cd into your server directory.
Then use ``curl`` or ``wget`` to update PocketMine-MP using the following command:

.. code-block:: sh

    curl -sL https://get.pmmp.io | bash -s - -u
    wget -q -O - https://get.pmmp.io | bash -s - -u


Manually update
---------------

Update PHP binary
+++++++++++++++++

1. Download the PHP binary for your OS (:ref:`Downloads <downloads>`)
2. Delete the ``bin`` directory in your server folder.
3. Extract the new PHP binary. You should see a new ``bin`` directory has been created.

Updating PocketMine-MP
++++++++++++++++++++++

1. Delete your current PocketMine-MP.phar
2. Download the updated PocketMine-MP phar you want to use (:ref:`Downloads <downloads>`)
3. Change the name to ``PocketMine-MP.phar``
4. Place it in the server folder

.. note:: Don't forget to rename the file to ``PocketMine-MP.phar``
