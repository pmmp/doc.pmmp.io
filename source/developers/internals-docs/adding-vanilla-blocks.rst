How to add a new *vanilla* block to PocketMine-MP
=================================================

Getting it working as a bare minimum
------------------------------------

1) Make the class (if it needs one) or choose one of the standard classes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using predefined block classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The majority of blocks don’t need a custom class, since they’re just
cubes. You can use ``Opaque`` or ``Transparent`` for these, depending on
what the block needs.

There are also standard classes for lots of common blocks that you can
use, such as ``Wall``, ``Door``, ``Stair``, ``Trapdoor`` etc.

Making a custom block class
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Custom block classes are only usually needed if a new block needs specific
properties (e.g. facing, age, etc), or if the block has special behaviour
or functionality (e.g. custom drops, ticking logic or interaction behaviour).

Predefined traits
+++++++++++++++++

There are many traits in the ``src/block/utils`` folder which add common
properties and/or behaviour to blocks (e.g. copper properties, facing).
Use these if they suit your needs.

.. note::
   Don’t forget to implement the related interfaces if you use a trait.

If none of the traits suit your purpose, you might need to add properties
of your own.

Defining your own properties
++++++++++++++++++++++++++++

This is pretty simple:

1. Define a `private` or `protected` field in the block class
2. Add a ``public`` getter and a ``public`` fluent setter for it (a setter that returns ``$this``). Don't forget to add validation to the setter where appropriate.
3. Track the property using ``describeBlockOnlyState()`` or ``describeBlockItemState()`` (see below).

+------------------------------+---------------------------------+------------------------------------------+
| Function                     | When block is obtained as item  | Examples                                 |
+==============================+=================================+==========================================+
| ``describeBlockOnlyState()`` | Properties are discarded        | facing, open/closed, powered, age        |
+------------------------------+---------------------------------+------------------------------------------+
| ``describeBlockItemState()`` | Properties are kept on the item | color, stripped (wood), copper oxidation |
+------------------------------+---------------------------------+------------------------------------------+

.. warning::
   If you don't track the property using one of the ``describe`` functions, its value won't be remembered across different ``getBlock()`` calls.

Adding custom behaviour
+++++++++++++++++++++++

There are many functions you can override to change the default behaviour of a block.
Some common ones include:

+---------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
| Function                        | Called when                                                                                           | Usage examples                                         |
+=================================+=======================================================================================================+========================================================+
| ``onInteract()``                | Player right-clicks or taps the block                                                                 | Opening inventory windows, opening/closing doors       |
+---------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
| ``place()``                     | Player tries to place the block                                                                       | Placing a block that faces a particular direction      |
+---------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
| ``onNearbyBlockChange()``       | Block nearby (or the block itself) recently changed                                                   | Torch self-destructing because its support was deleted |
+---------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
| ``getDropsForCompatibleTool()`` | Player breaks the block with the correct type and tier of tool                                        | Customising drops                                      |
+---------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
| ``onRandomTick()``              | Randomly when inside a player's simulation distance (requires ``ticksRandomly()`` to return ``true``) | Crop growth                                            |
+---------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------+
| ``onScheduledUpdate()``         | Delayed update was scheduled on the block                                                             | Liquid flow                                            |
+---------------------------------+-------------------------------------------------------------------------------------------------------+--------------------------------------------------------+

2) Register your block in ``src/block/VanillaBlocksInputs.php``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This will create a ``VanillaBlocks::YOUR_BLOCK()`` static method
automagically. In here, you’ll define properties like:

- The block’s name in English
- Hardness (affects the time to break)
- Best tool(s) to break the block with
- Required tool tier to get drops
- Explosion resistance (optional, defaults to hardness x5)

After you’ve registered your block in here, run
``composer update-codegen`` in your CLI. This will regenerate ``VanillaBlocks.php`` so your IDE knows 
about ``VanillaBlocks::YOUR_BLOCK()``.

3) Setup the block (de)serializer in ``src/data/bedrock/block/convert/VanillaBlockMappings.php``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There’s a few different ways you can do this.

Simple blocks (no properties)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most blocks have no properties. These can be added easily with
``BlockSerializerDeserializerRegistrar->mapSimple()``. You can just add
these to the list in
``VanillaBlockMappings::registerSimpleIdOnlyMappings()``.

Very common block types with properties (slabs, stairs)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``BlockSerializerDeserializerRegistrar`` has some other helpers for very
common block types, such as ``mapStairs()``, ``mapSlab()``. Use these if
you can.

Blocks with custom properties
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Blocks that have tags in their ``states`` NBT will usually require a
data model with property definitions to map their NBT onto your class.

If it’s a common type of block (e.g. stairs, doors, trapdoors, walls),
there might be common property definitions in ``CommonProperties``. For
example, registering a trapdoor looks like this (as of 5.33.2):

.. code:: php

   $reg->mapModel(Model::create(Blocks::IRON_TRAPDOOR(), Ids::IRON_TRAPDOOR)->properties($commonProperties->trapdoorProperties));

Always make sure to check the ``CommonProperties`` class first in case
there’s a common definition for the property you need.
``CommonProperties`` has lots of common definitions, such as for
horizontal facing, axis etc. and also definition arrays for things like
doors, walls, pressure plates, fence gates, stairs, etc.

If none of the ``CommonProperties`` definitions suit your needs, you can
define your own as shown below, and you can also combine them with the
common definitions.

.. code:: php

   $reg->mapModel(Model::create(Blocks::MY_TRAPDOOR(), Ids::MY_TRAPDOOR)->properties([
       ...$commonProperties->trapdoorProperties,
       new BoolProperty("nbt_property_name", fn(MyTrapdoor $b) => $b->isDoingSomething(), fn(MyTrapdoor $b, bool $v) => $b->setDoingSomething($v))
   ]);

There are various other classes of property descriptors available in the
``src/data/bedrock/block/convert/property`` folder to suit pretty much
every need, such as:

* ``BoolFromStringProperty`` - exactly what it sounds like
* ``ValueFromIntProperty`` - lets you map an ``IntTag`` to an ``enum`` or ``int``
* ``ValueFromStringProperty`` - same as above but for ``StringTag`` (commonly used for enumerated properties)
* ``ValueSetFromIntProperty`` - lets you turn a set of flags in an ``IntTag`` into an ``array<SomeValue>`` (used for chiseled bookshelf slots, vine faces, etc.)
* ``IntProperty`` - for integer ranges (e.g. redstone power level 0-15)

Blocks with properties baked into their IDs (flattened)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sometimes, Mojang decides to bake one or more propertes into the ID of a
block. This is commonly known as “flattening”.

Copper blocks are a particularly egregious example of this. There are 8
different IDs for each copper block: Normal, Exposed, Weathered,
Oxidised, and then waxed variants of each of these.

While we *could* define a new block type in each instance of this, it’d
be very inconvenient for implementing internal functionality, and it
would also suck for plugins. So instead we have a system for dealing
with them that works very similarly to parsing NBT properties:

.. code:: php

   $reg->mapFlattenedId(FlattenedIdModel::create(Blocks::SPONGE())->idComponents([
       "minecraft:",
       new BoolFromStringProperty("wet", "", "wet_", fn(Sponge $b) => $b->isWet(), fn(Sponge $b, bool $v) => $b->setWet($v)),
       "sponge"
   ]));

The ``idComponents()`` function accepts ``list<string|StringProperty>``,
so you can compose ID patterns using any number of properties and fixed
strings. This allows PocketMine-MP to implement blocks however we like
without being restricted by Mojang’s choice of data save structure.

As before, you may also find common ID components in
``CommonProperties``. For example, implementing a copper trapdoor looks
like this:

.. code:: php

   $reg->mapFlattenedId(FlattenedIdModel::create(Blocks::COPPER_TRAPDOOR())
       ->idComponents([...$commonProperties->copperIdPrefixes, "copper_trapdoor"])
       ->properties($commonProperties->trapdoorProperties)
   );

Blocks with one ID, but you want to split them into multiple PM blocks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is a rare case, but sometimes Mojang poorly implements a block such
that we want to split an ID into multiple blocks in order to provide a
more sensible API and/or to prevent undefined behaviour.

A great example of this is hanging signs, which have one ID
(per wood type), but actually have 3 distinct types with different
properties and behaviours:

- Ceiling center hanging sign has two chains connected to the center of the block above, and can face 16 ways
- Ceiling edges hanging sign can only face 4 ways, and its chains connect to the edges of the block above
- Wall signs can only face 4 ways and are self-supporting

If you find yourself in this position, have a look at how similar blocks
are handled in ``VanillaBlockMappings::registerSplitMappings()``.

Non-essential, but probably useful next steps
---------------------------------------------

Now you’ve done the essential stuff, you should now be able to boot up
the server and start testing the block(s) you just implemented.

However, there are a couple of extra steps that you should do.

Add a mapping to ``src/item/StringToItemParser.php``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This makes the block able to be given using the ``/give`` command and
commands like it, as well as for plugin configs.

This is super easy and will take you probably 10 seconds.

Define constant(s) in ``src/block/BlockTypeIds.php``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These let plugins identify your block easily using
``$block->getTypeId()``. If you don’t define constants, the server will
log a warning and generate a dynamic type ID for your block.

.. note::
    Don’t forget to update ``BlockTypeIds::FIRST_UNUSED_BLOCK_ID``!
