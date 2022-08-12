.. _corepermissions:

PocketMine-MP Core Permissions
==============================

Generated from PocketMine-MP 4.7.1+dev

.. list-table::
   :header-rows: 1

   * - Name
     - Description
     - Implied permissions

   * - ``pocketmine.broadcast.admin``
     - Allows the user to receive administrative broadcasts
     - N/A
   * - ``pocketmine.broadcast.user``
     - Allows the user to receive user broadcasts
     - N/A
   * - ``pocketmine.command.ban.ip``
     - Allows the user to ban IP addresses
     - N/A
   * - ``pocketmine.command.ban.list``
     - Allows the user to list banned players
     - N/A
   * - ``pocketmine.command.ban.player``
     - Allows the user to ban players
     - N/A
   * - ``pocketmine.command.clear.other``
     - Allows the user to clear inventory of other players
     - N/A
   * - ``pocketmine.command.clear.self``
     - Allows the user to clear their own inventory
     - N/A
   * - ``pocketmine.command.defaultgamemode``
     - Allows the user to change the default gamemode
     - N/A
   * - ``pocketmine.command.difficulty``
     - Allows the user to change the game difficulty
     - N/A
   * - ``pocketmine.command.dumpmemory``
     - Allows the user to dump memory contents
     - N/A
   * - ``pocketmine.command.effect``
     - Allows the user to give/take potion effects
     - N/A
   * - ``pocketmine.command.enchant``
     - Allows the user to enchant items
     - N/A
   * - ``pocketmine.command.gamemode``
     - Allows the user to change the gamemode of players
     - N/A
   * - ``pocketmine.command.gc``
     - Allows the user to fire garbage collection tasks
     - N/A
   * - ``pocketmine.command.give``
     - Allows the user to give items to players
     - N/A
   * - ``pocketmine.command.help``
     - Allows the user to view the help menu
     - N/A
   * - ``pocketmine.command.kick``
     - Allows the user to kick players
     - N/A
   * - ``pocketmine.command.kill.other``
     - Allows the user to kill other players
     - N/A
   * - ``pocketmine.command.kill.self``
     - Allows the user to commit suicide
     - N/A
   * - ``pocketmine.command.list``
     - Allows the user to list all online players
     - N/A
   * - ``pocketmine.command.me``
     - Allows the user to perform a chat action
     - N/A
   * - ``pocketmine.command.op.give``
     - Allows the user to give a player operator status
     - N/A
   * - ``pocketmine.command.op.take``
     - Allows the user to take a player's operator status
     - N/A
   * - ``pocketmine.command.particle``
     - Allows the user to create particle effects
     - N/A
   * - ``pocketmine.command.plugins``
     - Allows the user to view the list of plugins
     - N/A
   * - ``pocketmine.command.save.disable``
     - Allows the user to disable automatic saving
     - N/A
   * - ``pocketmine.command.save.enable``
     - Allows the user to enable automatic saving
     - N/A
   * - ``pocketmine.command.save.perform``
     - Allows the user to perform a manual save
     - N/A
   * - ``pocketmine.command.say``
     - Allows the user to talk as the console
     - N/A
   * - ``pocketmine.command.seed``
     - Allows the user to view the seed of the world
     - N/A
   * - ``pocketmine.command.setworldspawn``
     - Allows the user to change the world spawn
     - N/A
   * - ``pocketmine.command.spawnpoint``
     - Allows the user to change player's spawnpoint
     - N/A
   * - ``pocketmine.command.status``
     - Allows the user to view the server performance
     - N/A
   * - ``pocketmine.command.stop``
     - Allows the user to stop the server
     - N/A
   * - ``pocketmine.command.teleport``
     - Allows the user to teleport players
     - N/A
   * - ``pocketmine.command.tell``
     - Allows the user to privately message another player
     - N/A
   * - ``pocketmine.command.time.add``
     - Allows the user to fast-forward time
     - N/A
   * - ``pocketmine.command.time.query``
     - Allows the user query the time
     - N/A
   * - ``pocketmine.command.time.set``
     - Allows the user to change the time
     - N/A
   * - ``pocketmine.command.time.start``
     - Allows the user to restart the time
     - N/A
   * - ``pocketmine.command.time.stop``
     - Allows the user to stop the time
     - N/A
   * - ``pocketmine.command.timings``
     - Allows the user to record timings to analyse server performance
     - N/A
   * - ``pocketmine.command.title``
     - Allows the user to send a title to the specified player
     - N/A
   * - ``pocketmine.command.transferserver``
     - Allows the user to transfer self to another server
     - N/A
   * - ``pocketmine.command.unban.ip``
     - Allows the user to unban IP addresses
     - N/A
   * - ``pocketmine.command.unban.player``
     - Allows the user to unban players
     - N/A
   * - ``pocketmine.command.version``
     - Allows the user to view the version of the server
     - N/A
   * - ``pocketmine.command.whitelist.add``
     - Allows the user to add a player to the server whitelist
     - N/A
   * - ``pocketmine.command.whitelist.disable``
     - Allows the user to disable the server whitelist
     - N/A
   * - ``pocketmine.command.whitelist.enable``
     - Allows the user to enable the server whitelist
     - N/A
   * - ``pocketmine.command.whitelist.list``
     - Allows the user to list all players on the server whitelist
     - N/A
   * - ``pocketmine.command.whitelist.reload``
     - Allows the user to reload the server whitelist
     - N/A
   * - ``pocketmine.command.whitelist.remove``
     - Allows the user to remove a player from the server whitelist
     - N/A
   * - ``pocketmine.group.console``
     - Grants all console permissions
     - :ref:`Jump<permissions_implied_by_pocketmine.group.console>`
   * - ``pocketmine.group.operator``
     - Grants all operator permissions
     - :ref:`Jump<permissions_implied_by_pocketmine.group.operator>`
   * - ``pocketmine.group.user``
     - Grants all non-sensitive permissions that everyone gets by default
     - :ref:`Jump<permissions_implied_by_pocketmine.group.user>`


Implied permissions
-------------------

Some permissions automatically grant (or deny) other permissions by default when granted. These are referred to as **implied permissions**.

Permissions may imply permissions which in turn imply other permissions (e.g. ``pocketmine.group.operator`` implies ``pocketmine.group.user``, which in turn implies ``pocketmine.command.help``).

Implied permissions can be overridden by explicit permissions from elsewhere.

**Note:** When explicitly denied, implied permissions are inverted. This means that "granted" becomes "denied" and vice versa.



.. _permissions_implied_by_pocketmine.group.console:

Permissions implied by ``pocketmine.group.console``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users granted this permission will also be granted/denied the following permissions implicitly:

.. list-table::
   :header-rows: 1

   * - Name
     - Type
   * - ``pocketmine.command.dumpmemory``
     - Granted
   * - ``pocketmine.group.operator``
     - Granted

.. _permissions_implied_by_pocketmine.group.operator:

Permissions implied by ``pocketmine.group.operator``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users granted this permission will also be granted/denied the following permissions implicitly:

.. list-table::
   :header-rows: 1

   * - Name
     - Type
   * - ``pocketmine.broadcast.admin``
     - Granted
   * - ``pocketmine.command.ban.ip``
     - Granted
   * - ``pocketmine.command.ban.list``
     - Granted
   * - ``pocketmine.command.ban.player``
     - Granted
   * - ``pocketmine.command.clear.other``
     - Granted
   * - ``pocketmine.command.defaultgamemode``
     - Granted
   * - ``pocketmine.command.difficulty``
     - Granted
   * - ``pocketmine.command.effect``
     - Granted
   * - ``pocketmine.command.enchant``
     - Granted
   * - ``pocketmine.command.gamemode``
     - Granted
   * - ``pocketmine.command.gc``
     - Granted
   * - ``pocketmine.command.give``
     - Granted
   * - ``pocketmine.command.kick``
     - Granted
   * - ``pocketmine.command.kill.other``
     - Granted
   * - ``pocketmine.command.list``
     - Granted
   * - ``pocketmine.command.op.give``
     - Granted
   * - ``pocketmine.command.op.take``
     - Granted
   * - ``pocketmine.command.particle``
     - Granted
   * - ``pocketmine.command.plugins``
     - Granted
   * - ``pocketmine.command.save.disable``
     - Granted
   * - ``pocketmine.command.save.enable``
     - Granted
   * - ``pocketmine.command.save.perform``
     - Granted
   * - ``pocketmine.command.say``
     - Granted
   * - ``pocketmine.command.seed``
     - Granted
   * - ``pocketmine.command.setworldspawn``
     - Granted
   * - ``pocketmine.command.spawnpoint``
     - Granted
   * - ``pocketmine.command.status``
     - Granted
   * - ``pocketmine.command.stop``
     - Granted
   * - ``pocketmine.command.teleport``
     - Granted
   * - ``pocketmine.command.time.add``
     - Granted
   * - ``pocketmine.command.time.query``
     - Granted
   * - ``pocketmine.command.time.set``
     - Granted
   * - ``pocketmine.command.time.start``
     - Granted
   * - ``pocketmine.command.time.stop``
     - Granted
   * - ``pocketmine.command.timings``
     - Granted
   * - ``pocketmine.command.title``
     - Granted
   * - ``pocketmine.command.transferserver``
     - Granted
   * - ``pocketmine.command.unban.ip``
     - Granted
   * - ``pocketmine.command.unban.player``
     - Granted
   * - ``pocketmine.command.whitelist.add``
     - Granted
   * - ``pocketmine.command.whitelist.disable``
     - Granted
   * - ``pocketmine.command.whitelist.enable``
     - Granted
   * - ``pocketmine.command.whitelist.list``
     - Granted
   * - ``pocketmine.command.whitelist.reload``
     - Granted
   * - ``pocketmine.command.whitelist.remove``
     - Granted
   * - ``pocketmine.group.user``
     - Granted

.. _permissions_implied_by_pocketmine.group.user:

Permissions implied by ``pocketmine.group.user``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users granted this permission will also be granted/denied the following permissions implicitly:

.. list-table::
   :header-rows: 1

   * - Name
     - Type
   * - ``pocketmine.broadcast.user``
     - Granted
   * - ``pocketmine.command.clear.self``
     - Granted
   * - ``pocketmine.command.help``
     - Granted
   * - ``pocketmine.command.kill.self``
     - Granted
   * - ``pocketmine.command.me``
     - Granted
   * - ``pocketmine.command.tell``
     - Granted
   * - ``pocketmine.command.version``
     - Granted

