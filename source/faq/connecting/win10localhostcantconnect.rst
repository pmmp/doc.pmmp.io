Minecraft can't connect to a server on the same computer on Windows
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. note::

    These steps are **not** required to connect to all servers. You only need to do this if you're connecting to a server on the  **same computer** that you're running Minecraft on.

Disable UWP loopback restrictions for Minecraft
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Windows UWP apps have some restrictions on what they are allowed to do by default.
Unfortunately, this includes connecting to things on localhost.

To lift this restriction from Minecraft, launch Windows PowerShell as an administrator and run the following:

.. code-block:: sh

    CheckNetIsolation LoopbackExempt -a -n="Microsoft.MinecraftUWP_8wekyb3d8bbwe"

If everything goes well, you'll see a message: ``OK.`` You should now be able to connect (you may need to close and reopen the game).

Don't use ``localhost`` for server address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Minecraft for Windows doesn't correctly handle the ``localhost`` address.

Try using ``127.0.0.1`` (IPv4) or ``::1`` (IPv6) instead when adding the server to your server list.

