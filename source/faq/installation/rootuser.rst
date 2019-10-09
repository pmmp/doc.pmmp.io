Can't install as user root
""""""""""""""""""""""""""

.. warning::

    Running the installer as root is **strongly discouraged**.

    Bugs in the installer have previously caused **loss of data** for people who ran it as root.

    It is recommended to run it as a normal user as it doesn't need further permissions.

We recommend you to install PocketMine-MP as a normal user, not as root. 
Create one if you don't have one.

.. code-block:: sh

    useradd -d /home/pocketmine -m pocketmine
    passwd pocketmine
