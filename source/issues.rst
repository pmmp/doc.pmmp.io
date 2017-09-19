.. _issues:

Issues
======

Did your server crash, or did you encounter a bug?

- Make sure you're using the latest available version of PocketMine-MP, as the bug might already have been fixed.
- Try and reproduce it **WITHOUT PLUGINS**, as plugins can frequently cause issues.
- Ask for help on our `forums`_ before creating an issue.

.. warning::
	Please **do not** use our issue tracker for support requests, but instead seek assistance on the `forums`_. Support request issues will be closed as per the contribution guidelines.

.. note::
	Make sure you read the `contribution guidelines <https://github.com/pmmp/PocketMine-MP/blob/master/CONTRIBUTING.md#creating-an-issue>`_ before creating an issue.

If your issue is still unresolved and you're sure the issue is caused by PocketMine-MP itself, then `make a new issue <https://github.com/pmmp/PocketMine-MP/issues/new>`_ on GitHub.

Issue template
~~~~~~~~~~~~~~

An issue template is provided, showing the information that we require for an issue submission. **Do not** just delete the template - fill it with the information it asks for.
Give as much information as you can about when or what happened.

.. image:: /img/create-issue.png

Crashdumps
~~~~~~~~~~

Did the server crash and generate a crash dump?
When the server creates a crashdump, it attempts to send it to our crash archive (unless the user disables this in their pocketmine.yml).

If it succeeds, you will see a message like this:
``[18:34:15] [Server thread/EMERGENCY]: The crash dump has been automatically submitted to the Crash Archive. You can view it on https://crash.pmmp.io/view/5555 or use the ID #5555.``

When you create your issue, please include the link to your crashdump to help us diagnose the problem.

If you don't have a link but have a crashdump, you can submit it manually at https://crash.pmmp.io/submit

.. error::
	Please **DO NOT** paste crashdump contents into an issue. Upload it to the `Crash Archive <https://crash.pmmp.io/submit>`_ instead.

.. _forums: https://forums.pmmp.io/forums/help/
