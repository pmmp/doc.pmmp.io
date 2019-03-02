.. _crashes:

Crashes
=======

PocketMine-MP may crash for a number of reasons:

- Bad / faulty plugins.
- Running out of memory due to not enough or memory leak.
- Bugs within the PocketMine-MP which are unrecoverable.

In all of the above cases, a crashdump file will be generated in the ``crashdumps`` folder of your server.


Reporting a crash
~~~~~~~~~~~~~~~~~
Crash reports are automatically submitted to our `Crash Archive`_ if your server is connected to the internet.

If successful, you will see a message like this in the server log:
``[18:34:15] [Server thread/EMERGENCY]: The crash dump has been automatically submitted to the Crash Archive. You can view it on https://crash.pmmp.io/view/5555 or use the ID #5555.``

If you want to submit a crash report manually, you can do so at the `submit page <https://crash.pmmp.io/submit>`_.

Crashdumps are searched and investigated regularly by the development team, so it is not necessary to submit an issue if your crashdump is in the `Crash Archive`_.
Nonetheless, you can create one anyway at the `issues page <https://github.com/pmmp/PocketMine-MP/issues/new/choose>`_ if you want to give us extra information or draw our attention to the issue.

.. note::

    If you want to opt-out of automatic crashdump submission, you can disable it using the ``auto-report.enabled`` setting in your ``pocketmine.yml``.
	
.. warning::

    When reporting a crash in PocketMine-MP, a crashdump file **must** be provided or we will not be able to help you.

What's in a crashdump file?
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Crashdumps are ``.log`` files which contain important information which is used to identify, reproduce, and fix bugs. They contain human-readable information about the crash (the top part) and a machine-readable part which is used by our `Crash Archive`_.

A crashdump may contain the following information:

- Error message, file name, line number and error type
- A stack trace of the error, which helps identify where the crash happened
- A sample of code around the site of the crash, which helps to identify where the crash happened
- Information about your operating system version and hardware (such as CPU model)
- List of plugins installed on the server
- Version of PocketMine-MP which you are using
- The contents of your ``pocketmine.yml`` and ``server.properties`` file (sensitive information like passwords are redacted)

.. note::

    You can fine-tune what information is placed in crashdumps in your ``pocketmine.yml`` file under the ``auto-report`` section.


.. _Crash Archive: https://crash.pmmp.io
