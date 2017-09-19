Links
-----

.. _downloads:

Downloads
=========

PocketMine-MP prebuilt phars
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
There are 4 available channels for downloads (ordered least stable to most stable):

- `Development (least stable, produced for every commit to master) <https://jenkins.pmmp.io/job/PocketMine-MP/Development/>`_
- `Alpha (lacking planned features, may be unstable) <https://jenkins.pmmp.io/job/PocketMine-MP/Alpha>`_
- `Beta (may be unstable) <https://jenkins.pmmp.io/job/PocketMine-MP/Beta/>`_
- `Stable <https://jenkins.pmmp.io/job/PocketMine-MP/Stable/>`_

You are recommended to take the most stable build which is compatible with your Minecraft version. You can see the compatible Minecraft version and other information by looking at the ``build_info.json`` file in the artifacts.

.. warning::
	**Do not use development builds** unless there is no other option available, since these will undergo breaking changes without notice from build to build.
	You are recommended to use Alpha, Beta or Stable builds, as those are in a known state and all the changes for those are fully documented.

.. note::
	The links above may yield "404 Not Found" if no build is available in that channel.
	At the time of writing, only Development and Alpha builds are currently available since PocketMine-MP is currently under heavy development. You are currently recommended to take Alpha builds or better.

.. note::
	Compatible DevTools phars are also shipped in every PocketMine-MP build from our Jenkins server.


Linux & MacOS installer script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* `Linux & MacOS install script source <https://raw.githubusercontent.com/pmmp/php-build-scripts/master/installer.sh>`_

Prebuilt PHP binaries and related packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. note::
	If there are no prebuilt binaries of the version you want available for your platform, you may be able to build your own using our `compile scripts`_.

Linux
*****
- `PHP 7.2 <https://jenkins.pmmp.io/job/PHP-7.2-Linux-x86_64/>`_
- `PHP 7.0 (legacy) <https://jenkins.pmmp.io/job/PHP-7.0-Linux-x86_64/>`_

MacOS
*****
- PHP 7.2 - No PHP 7.2 prebuilt binaries are available for MacOS yet.
- `PHP 7.0 (legacy) <https://bintray.com/pocketmine/PocketMine/Unix-PHP-Binaries/view#files>`_

Windows
*******
.. note::
	All Windows builds can be found on AppVeyor. The build versions are in the format ``php-[php major version]-appveyor[build#]``, for example ``php-7.2-appveyor95``. Click the latest build with the PHP version you want, click Artifacts and download the zip.


- `PHP (AppVeyor) <https://ci.appveyor.com/project/pmmp/php-build-scripts/history>`_
- `Microsoft Visual C++ 2017 Redistributable <https://support.microsoft.com/en-gb/help/2977003/the-latest-supported-visual-c-downloads>`_


Other links
===========
* `PMMP GitHub organisation <https://www.github.com/pmmp/>`_
* `PocketMine-MP GitHub repository <https://github.com/pmmp/pocketmine-mp>`_
* `PHP compile scripts <https://github.com/pmmp/php-build-scripts>`_
* `PMMP Website <https://pmmp.io/>`_
* `PMMP Forums <https://forums.pmmp.io>`_
* `PocketMine-MP Translation Project <http://translate.pocketmine.net/>`_

.. _compile scripts: https://github.com/pmmp/php-build-scripts