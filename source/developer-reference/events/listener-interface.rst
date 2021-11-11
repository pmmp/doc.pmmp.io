.. _listener_interface:

Using the ``pocketmine\event\Listener`` interface
=================================================

This interface is implemented by classes which want to have matching methods within themselves (and their child classes) to be treated as event handlers on registration. Every method in a ``Listener``-implementing class is checked as a candidate event handler.

How does it work?
+++++++++++++++++

When you call ``registerEvents()``, PocketMine-MP does some complicated `reflection <https://www.php.net/manual/en/book.reflection.php>`_ magic to examine the functions declared in the given listener object.
It then adds any function that meets the criteria below to the handler list for the desired event.

The type of event handled by a function is decided by the type of the first parameter.

.. note::

    Handler function names are **completely ignored**. Therefore, it doesn't matter whether your handler is called ``onPlayerJoin()`` or ``iEatEnglishForBreakfast()``; as long as the function meets the required criteria described below, it will be registered.

What counts as a handler method?
++++++++++++++++++++++++++++++++

To be considered as an event handler candidate, a ``Listener`` method MUST meet the below criteria:

- MUST accept exactly ONE parameter
- This one parameter MUST be a class extending ``pocketmine\event\Event`` which is either non-abstract or declares the ``@allowHandle`` in the class doc comment.
- MUST be public
- MUST NOT be static
- MUST be declared by a class implementing ``Listener`` or extending a class which implements ``Listener`` (i.e. a method in a non-``Listener``-implementing base class which meets the above criteria IS NOT be considered a handler)
- MUST NOT declare the ``@notHandler`` PhpDoc annotation (will be ignored if it does)

The following are not mandatory but recommended:

- SHOULD NOT return a value (recommended to have a ``void`` return type (this may become a requirement in future))
- SHOULD NOT handle an event marked as ``@deprecated``

Annotations controlling a handler function's behaviour
++++++++++++++++++++++++++++++++++++++++++++++++++++++

Event handlers within a ``Listener`` can have their behaviour altered using certain PhpDoc doc-comment tags (otherwise known as "annotations").
The following annotations are respected for candidate handlers:

- ``@notHandler``: Marks a function as explicitly NOT being an event handler, even if it meets all other criteria.
- ``@ignoreCancelled``: This handler WILL NOT receive events which are cancelled before reaching it.
- ``@priority``: Allows controlling when in the event calling sequence this handler will be executed. This allows competing handlers of the same event to cooperate to some extent. See the section below on event priority. Example: ``@priority NORMAL``
- ``@softDepend``: Skips registering the handler if the event class it wants to handle does not exist. This can be used to soft-depend on classes provided by other plugins. Example: ``@softDepend SimpleAuth``
