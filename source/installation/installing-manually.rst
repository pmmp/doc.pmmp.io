.. _installing-manually:

Installing manually
-------------------

No installer available for your platform? Did the installer fail? It is not your taste? YOLO? DIY!

Getting PHP for your server
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Download your flavor PHP binary (:ref:`Downloads <downloads>`)
2. Extract the PHP binary into your server directory. If everything went well, you should have a `bin` folder in your server directory.
3. (Windows only) Download and install Microsoft Visual C++ Redistributable 2017 (:ref:`Downloads <downloads>`)

Getting PocketMine-MP
~~~~~~~~~~~~~~~~~~~~~

Using .phar
***********

1. Create a new directory for PocketMine-MP.
2. Download PocketMine-MP.phar (:ref:`Downloads <downloads>`)
3. Rename the .phar to ``PocketMine-MP.phar``.
4. Place it in the PocketMine-MP directory you just created.
5. Get the start script for your platform (`Windows CMD <https://github.com/pmmp/PocketMine-MP/blob/master/start.cmd>`_, `Windows PowerShell <https://github.com/pmmp/PocketMine-MP/blob/master/start.ps1>`_, `Linux/MacOS bash <https://github.com/pmmp/PocketMine-MP/blob/master/start.sh>`_)
6. (Linux/MacOS only) Make start.sh executable (chmod +x start.sh)

.. _install-using-git:

Using Git
*********

You can also run PocketMine-MP from source code by cloning the GitHub repository using Git.

PocketMine-MP uses Composer to manage its library dependencies. Composer is shipped with our prebuilt PHP packages, but if you want to install it manually, you can do so at https://getcomposer.org.

Clone the repository (recursively, to include submodules):

.. code::

    git clone https://github.com/pmmp/pocketmine-mp.git --recursive # don't forget the --recursive flag!

Install dependencies using Composer

- Basic version:

    .. code::

        path/to/php path/to/composer.phar install

- or, if you have a global Composer installation:

    .. code::

        composer install

- or, if you're using a prebuilt PHP provided by PMMP, a wrapper for Composer is provided:

    .. code::

        bin/composer install

If you're running a production server, you might want to skip dev dependencies and generate a faster autoloader:

    .. code::

        bin/composer install --no-dev --classmap-authoritative

See the docs at https://getcomposer.org for more information on using Composer.

.. warning::
    Remember to clone with the ``--recursive`` flag! PocketMine-MP has several submodules which are required to run the server.

    If you forgot the ``--recursive`` flag when you cloned, you can cd into the server directory and run ``git submodule update --init --recursive``.

.. warning::
	If running a production server, consider using a phar instead for better performance.

.. _GitHub: https://github.com/pmmp/pocketmine-mp/releases
.. _Crowdin: http://translate.pocketmine.net
.. _License: https://github.com/pmmp/pocketmine-mp/blob/master/LICENSE
