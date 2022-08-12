.. _permissions:

Permissions
===========

PocketMine-MP includes a powerful permission system, similar in functionality to the one found in Bukkit. It allows fine-grained control of access to various parts of the server functionality, such as:

* Ability to use individual commands
* Whether or not the user can see administrative broadcasts when a command is used (e.g. when someone uses ``/op``)

In addition, plugins can offer permissions to allow customising access to behaviours that they offer.

PocketMine-MP doesn't directly offer any way to use permissions at the time of writing (August 2022), but you can find permission management plugins in the "Admin Tools" section on Poggit.

- :ref:`List of PocketMine-MP core permissions <corepermissions>`

Names
-----

Permissions are referred to by names, which usually look something like ``pocketmine.command.help``.

There's no special requirements on permission names, but the de facto standard in community plugins is to separate the parts using ``.``, and use a common prefix for permissions for similar things. For example all PocketMine-MP core commands have permissions using the prefix ``pocketmine.command.``.

Grouping permission nodes together
----------------------------------

While most permissions affect one specific thing (e.g. whether or not a player is allowed to use a command), permissions may also automatically grant (or deny) other permissions when assigned. These special permissions are known as "group permissions".

An example of a group permission is ``pocketmine.group.operator``, which, when granted, grants permissions such as ``pocketmine.command.op.give`` which enable access to operator commands.

This is useful if you want to assign the same set of permissions to multiple users (or other groups).

Permission precedence
---------------------

Because of group permissions, it's possible that a user may receive multiple conflicting values for the same permission.

Permission values are resolved in the following order:

* Explicitly overridden permissions take maximum priority. This means that, for example, a player can receive ``pocketmine.group.operator``, but be denied ``pocketmine.command.op.give``, allowing them access to all operator commands **except** ``/op``.
* If the permission is not overridden directly, the value from the most recently assigned group permission will be used.
