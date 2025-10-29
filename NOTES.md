# Notes

My notes on modding splash damage, it's super complicated.

### ``Properties.txt``

Defines the property name and links it to an ``ItemStatCost.txt`` row.

- ``splash`` -> ``item_splashonhit``
- ``corruption`` -> ``item_iscorrupted``

### ``ItemStatCost.txt``

References ``splashdamage`` and ``corruption`` which are strings in ``patchstring.tbl`` (D2LOD) and ``item-modifiers.json`` (D2R).  These are just the description strings to appear in items.

- ``item_splashonhit`` -> ``splashdamage``
- ``item_iscorrupted`` -> ``corruption``

### ``AutoMagic.txt``

This is the table that assigns properties to items that spawn.  The files ``Weapons.txt``, ``UniqueItems.txt``, ``SetItems.txt`` reference back to this and invoke this.

- ``Quartermaster’s`` -> ``replenishing``
- ``Brute’s`` -> ``splash``
- ``Combo Weaps`` -> ``splash + replenishing``
- ``Splash+Replenishing Harpoonist's`` -> ``skills + splash + replenishing``
- ``Splash+Replenishing Spearmaiden's`` -> ``skills + splash + replenishing``
- ``Splash+Replenishing Lancer's`` -> ``skills + splash + replenishing``
- ``Splash Harpoonist's`` -> ``skills + splash``
- ``Splash Spearmaiden's`` -> ``skills + splash``
- ``Splash Lancer's`` -> ``skills + splash``

You need a property value ``splash``, a param value ``proc_SplashDamage`` (or ``371``the ID), and a minimum value ``100`` for this to work.

### ``Weapons.txt``, ``UniqueItems.txt``, ``SetItems.txt``

Uses ``autoaffix`` column and the ``351-354`` values referencing the ID in ``automagic.txt``.  Leave these alone.

### ``Skills.txt``

The ``autoaffix.txt`` file added to the item both a property ``splash`` and a parameter ``proc_SplashDamage``.  The ``proc_SplashDamage`` is the name of the skill in ``skills.txt``.

This row tells the skill what missle to use (``proc_splashdamage`` lowercase), how many missles to make, etc.

### ``Missiles.txt``

This fires off the actual missles.  The most important value in here is ``SrcDamage`` which determines how much damage the missle does.  A value of ``128`` is 100%, while ``64`` is 50%.

There is a ``nextHit`` value that make's it so a mob can't be hit by another projective for a moment.  So far a I can tell, from watching closely, I don't think the splash causes double damage to the mob you are hitting bc with fire enchanted charms I only see them spark a single time.

I have a ``proc_splashinit`` in here but it doesn't look like it's used anywhere.  Not sure where I got that from.