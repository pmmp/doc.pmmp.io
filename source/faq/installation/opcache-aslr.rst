Opcache Opcode handlers are unusable due to ASLR
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This happens when multiple different PHP binaries are used to run multiple servers on the same Windows computer.

To fix this problem, edit `bin/php/php.ini` with Notepad and add the following:

.. code-block:: ini

        opcache.cache_id=PHP_BINARY

Repeat this for every PHP binary you're using for PocketMine-MP.
