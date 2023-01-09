Stuck on "Locating server" or at downloading resource packs
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

.. note::

   This page includes some **possible workarounds**. It's not guaranteed that any of these suggestions will fix your problem.

Try a different network
+++++++++++++++++++++++

This usually indicates a problem with your connection. Try using an alternate WiFi network, LAN, mobile data, etc.

Possible workaround: Lower the server's max MTU size
++++++++++++++++++++++++++++++++++++++++++++++++++++

If you consistently have issues connecting to certain servers, sometimes broken MTU size discovery is at fault. This can be caused by an old device, old router, outdated software, or strange network settings.

If you're not able to fix this at the source, but you're able to access the server's ``pocketmine.yml``, you can try reducing the ``network.max-mtu-size``. Decrease it slowly (e.g. by 100 at a time), and test the server again each time to see if you can connect.

If you decrease the setting to around 600 and the problem still persists, the issue is likely not the MTU size.

.. note::

    While reducing the MTU size might enable you to connect, doing so is a **workaround** and will increase the bandwidth usage of your server. The reduced max MTU size will apply to every player, decreasing bandwidth efficiency.
    You should still try and find and fix the cause of the problem even if lowering the max MTU allows you to connect.

Remove large resource packs
+++++++++++++++++++++++++++

PocketMine-MP is currently known to have problems when using large resource packs on the server.

If you're having connection issues when using large packs (e.g. larger than 1 MB), try removing the packs and see if you can connect.
