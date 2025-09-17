.. _event_handler_priority:

Event handler priority
======================

Event "priority" is used to control the order in which multiple handlers of the same event will execute. This is mainly used for plugin interoperability.
The ``pocketmine\event\EventPriority`` class declares a series of hardcoded priorities which handlers can use.

.. note::

    Priority is a misleading name, because higher "priority" means that the handler should execute *later* in the sequence and not earlier. The reasoning for this is that higher order handlers "get the last word" over lower order handlers. This naming may be changed in future PocketMine-MP versions.

List of priorities
++++++++++++++++++

At the time of writing, the following priorities exist:

======= ===========
Name    Description
======= ===========
LOWEST  These handlers will be executed first.

        This should be used when the original event state is needed (before later handlers modify it),

        or when the handler is making a low-priority modification (to allow other handlers to override it).
LOW
NORMAL  If a priority is not specified, handlers will be registered here by default.
HIGH
HIGHEST Handlers registered at this priority get the final say in the event's outcome.
MONITOR These handlers will execute last.

        **No modification to the event's outcome should be made at this priority, including cancellation**.

        This should be used to only for **monitoring the outcome** of an event.
======= ===========

.. warning::

    When multiple handlers are registered to the same priority, the order of execution is undefined.
