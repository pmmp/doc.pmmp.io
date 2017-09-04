Commands
--------

.. note::
    This example was last updated for API **3.0.0-ALPHA7** and may be outdated and/or not work correctly. Please feel free to make a GitHub pull request if you find problems with it.

.. code-block:: yaml

    name: Example
    main: Example\Example
    version: 1.0.0
    api: 3.0.0-ALPHA7

    commands:
     example1:
      description: "Example1 command"
      usage: "/example1"
     example2:
      description: "Example2 command with arguments"
      usage: "/example2 <args>"


.. code-block:: php
    :linenos:

    <?php

    namespace Example;

    use pocketmine\plugin\PluginBase;
    use pocketmine\command\Command;
    use pocketmine\command\CommandSender;

    class Example extends PluginBase{

        public function onCommand(CommandSender $sender, Command $command, string $label, array $args) : bool{
            switch($command->getName()){
                case "example1":
                    // do stuff
                    return true;
                case "example2":
                    if (count($args) === 0){
                        return false;
                    }
                    var_dump($args); // do stuff
                    return true;
            }

            return false; //don't forget the return!
        }
    }
