.. _requirements:

Requirements
============

Setup requirements
------------------

* PHP 7.2 64-bit with the extensions needed for PocketMine-MP (you can download a prebuilt PHP, or you can build PHP with the extensions required using our custom `compile scripts`_)
* Latest PocketMine-MP phar compatible with your MCPE version
* Dual-core or better processor is recommended. For best performance choose high clock frequency over core count
* 1GB RAM or better

We officially try to support Windows, Linux and MacOS platforms. However, in general any platform which will run 64-bit PHP with the required extensions will work.

.. error::
	PocketMine-MP is not supported on 32-bit systems.

.. warning::
	Windows additionally requires *Microsoft Visual C++ 2017 Redistributable* to be installed for PHP to run. You can download it from the `Microsoft website`_.

Download links
--------------

* `PocketMine-MP.phar`_
* `Linux/MacOS install script`_
* `Windows PHP binaries`_
* `Linux PHP binaries`_
* `MacOS PHP binaries`_

.. _compile scripts: https://github.com/pmmp/php-build-scripts
.. _Microsoft website: https://support.microsoft.com/en-gb/help/2977003/the-latest-supported-visual-c-downloads
.. _Linux/MacOS install script: https://raw.githubusercontent.com/pmmp/php-build-scripts/master/installer.sh
.. _Windows PHP binaries: https://ci.appveyor.com/project/pmmp/php-build-scripts/build/artifacts
.. _Linux PHP binaries: https://jenkins.pmmp.io/job/PHP-7.2-Linux-x86_64/
.. _MacOS PHP binaries: https://bintray.com/pocketmine/PocketMine/Unix-PHP-Binaries/view#files
.. _PocketMine-MP.phar: https://jenkins.pmmp.io/job/PocketMine-MP/
