.. _resourcepacks:

Resource Packs & Behaviour Packs
================================

PocketMine-MP has some support for resource packs.

Any number of valid resource packs may be loaded. However, per-world resource packs are not currently supported at the time of writing.

.. error::

	Behaviour packs are **not** supported.

.. warning::

	Resource packs which **depend on behaviour packs** may not work correctly. While PocketMine-MP will not prevent you loading such packs, it makes no attempt to validate dependencies and your game may experience errors or crashes when attempting to use them.

Installing resource packs
~~~~~~~~~~~~~~~~~~~~~~~~~

Resource packs to be loaded should be placed in the ``resource_packs`` folder of your server data.

Then, you will need to add them to the stack in the ``resource_packs.yml`` file (also located in the ``resource_packs`` folder).


Resource stack
~~~~~~~~~~~~~~

This is a list of resource packs in ``resource_packs.yml`` that will used by your server. It should contain a list of valid resource pack file names found in the ``resource_packs`` folder, including the file extension.

Resource packs are applied from bottom to top, similar to how they work in Minecraft itself. This means that resources at the top of the list will override resources lower down the list.


Supported pack formats
~~~~~~~~~~~~~~~~~~~~~~

At the time of writing, the following types of resource pack are supported:

- ``.zip``
- ``.mcpack``

.. error::

	Unpacked (folder) resource packs are not currently supported.
