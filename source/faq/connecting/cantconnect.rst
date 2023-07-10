Can't connect to the server after updating Minecraft
""""""""""""""""""""""""""""""""""""""""""""""""""""

Newer versions of Minecraft Bedrock often bring breaking network changes unpredictably.
If you are unable to connect after updating your version, it is likely that you need to update your server version to a newer one that supports the version you're trying to connect with.

Often, **but not always**, newer patch versions (e.g. 1.20.0, 1.20.1) are compatible without any update needed. Look for the latest version which offers a version less than or equal to yours.

Run the ``version`` command to check the supported Minecraft version of your server.

Example:

.. code-block:: log

    Command output | This server is running PocketMine-MP
    Command output | Server version: 5.2.0 (git hash: e6de9a70a211e1c2f4472dc2c4a0155ba0ffa5b2)
    Command output | Compatible Minecraft version: 1.20.0 (protocol version: 589)
    Command output | PHP version: 8.1.20
    Command output | PHP JIT: not supported
    Command output | Operating system: linux
