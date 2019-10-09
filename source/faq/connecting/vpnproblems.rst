VPN connection and gameplay issues
""""""""""""""""""""""""""""""""""

Minecraft Bedrock commonly has trouble with VPNs for reasons which are not entirely clear.

Make sure all MTU limits are set correctly
++++++++++++++++++++++++++++++++++++++++++

A common cause of VPN issues is incorrect, inconsistent or too-large tunnel or link MTUs. You can try testing with smaller MTU sizes and see if the problem goes away.

Reduce maximum MTU in PocketMine-MP itself
++++++++++++++++++++++++++++++++++++++++++

If you are not able to alter your VPN MTU sizes, you can try reducing the ``network.max-mtu-size`` setting in your ``pocketmine.yml`` file.
The default setting is 1492 - you may have success with smaller sizes.

.. note::

	While a smaller MTU may fix your connection issues, it also reduces efficiency, which may cause higher bandwidth consumption and higher data usage.