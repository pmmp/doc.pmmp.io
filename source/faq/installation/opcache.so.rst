Failed loading opcache.so (or other PHP extensions)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This may happen when the installer is not used or when PocketMine-MP was moved.

To fix this issue, run the following from wherever your PHP bin directory is:

.. code-block:: sh

	EXTENSION_DIR=$(find "$(pwd)/bin" -name *debug-zts*)
	grep -q '^extension_dir' bin/php7/bin/php.ini && sed -i'bak' "s{^extension_dir=.*{extension_dir=\"$EXTENSION_DIR\"{" bin/php7/bin/php.ini || echo "extension_dir=\"$EXTENSION_DIR\"" >> bin/php7/bin/php.ini

This will locate your PHP binary's extension_dir on the disk and set it into php.ini, replacing it if it already exists, and adding it if not.