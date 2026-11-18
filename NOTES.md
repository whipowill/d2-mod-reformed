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

# Port notes (2026-11)

Changes first made and tested in the play install, then copied into `D2LOD/Data`. D2R is NOT done, see `TODO.md`.

## Worldstone Shard is its own item

The shard used to be the Rancid Gas Potion (`gps`) row of ``Weapons.txt`` re-typed as a misc item, and the other five throwing potions (``gpm gpl ops opm opl``) were re-typed too. Now:

- ``Weapons.txt``: all six potion rows are the original game's.
- ``Misc.txt``: new LAST row ``wss`` (type ``misc``, level 24, cost 24000, ``invfile invwss``, ``flippyfile flpgsr``, 1x1, gem-style ``alternategfx gsw`` / ``component 16``, ``namestr wss``). Appended at the end so no item index moves.
- ``patchstring.tbl``: key ``wss`` = "Worldstone Shard".
- ``TreasureClassEx.txt``: class ``Orbs`` has ``wss`` as Item1; ``Misc 0/1/2`` are stock again (potions drop).
- ``CubeMain.txt``: the shard recipes use ``wss``. The original cow-level recipe (Wirt's Leg + Town Portal tome) is kept next to the single-input one.
- ``BH.cfg``: ``ItemDisplay[gps]`` -> ``ItemDisplay[wss]``. The empty ``ItemDisplay[...]`` lines for the five other potions still hide them; the commented originals are further down.

**Never change what an existing item code IS.** A saved item stores its code plus a layout that depends on the item's table row (type, stackable, durability). Turning `gps` back into a stackable potion made every saved shard unreadable: `Error Loading: <char> Error:14`, and no character loaded, because all of them load the PlugY shared stash. A new code appended at the end of ``Misc.txt`` is safe; re-typing an existing one is not. Saves still holding shards as `gps` must be converted to `wss` (same layout, only the 4-letter code changes) or the records removed (PlugY `.sss`/`.d2x`: delete the `JM` record and lower the page's u16 item count).

## Weapon reach (``rangeadder`` in ``Weapons.txt``)

Never lowers an existing value (201 of 231 melee/thrown weapons went up). Read from the table at run time, so it also affects existing items and is safe for saves.

| weapons | rangeadder |
|---|---|
| daggers (`knif`), throwing knives/axes (`tkni`, `taxe`) | 1 |
| one-handed melee (swords, axes, maces, clubs, scepters, hammers, claws `h2h`/`h2h2`) | 2 |
| two-handed swings (`2handed=1`) and javelins (`jave`, `ajav`) | 3 |
| spears (`spea`, `aspe`) and polearms (`pole`, incl. scythes) | 4 |
| bows, crossbows, Amazon bows, wands, orbs | untouched (0) |

Matches PD2 on 284 of 306 weapons. The differences are PD2 one-offs. PD2's damage, durability and strength changes and its `sc9` scythe type were not copied.

## Mercenaries

- The hire screen shows text only for HireDesc index 0-8 (a hard-coded 9-slot table), mapped to string ids 3371/3372, 11090/11088/11089, 3377/3376/3375. Labels use the form `Name (Aura)`. The ids 3371 3372 3375-3377 live in a loose `local/lng/eng/string.tbl` (overrides the MPQ copy); 11088-11090 in ``patchstring.tbl``.
- Act 2 "Combat" rows were removed (12 rows); Act 5 lost Battle Orders (Whirlwind moved to skill slot 2).
- ``States.txt``: the six `shrine_*` rows have the `curse` flag cleared.
- **A bad .tbl CRC crashes the game on load** (D2Lang CRC-16, init 0xFFFF, over [dataStart, fileEnd)).
- Act 5 merc Whirlwind needs no custom skill or sequence: stock player `Whirlwind` (id 151) and stock `seq_ancientwhirlwind` (``Sk1lvl=15`` on act5hire1/2). The data must add `Skill1=Whirlwind` in ``MonStats.txt`` and Whirlwind in ``Hireling.txt`` (stock Act 5 merc: Bash, Stun). The spin's behavior (starts in melee reach, travels through the pack, passes through monsters) comes from `qol.dll` (`[mercenary] whirlwind`, d2-mod-qol), not from data. The Fire Enchanted explosion fix and merc equipment/drop-items are also qol.dll in-memory patches.
- Deliberately not copied into the repo: loose `MonSeq.txt`, `BaseMod.tbl`, `font16.dc6`, the intro `.bik` videos (~450 MB), backup/lock files, generated `.bin` tables.

## Still to port to D2R

See `TODO.md`. D2R `weapons.txt` already has a `rangeadder` column (index 22) and the gas potions are still stock `tpot` rows, so the shard needs its own check against D2R's item definitions.

## Merc skill chances (Hireling.txt)

- For every merc row the chances add up to 100: `DefaultChance` (plain weapon attack) + aura + skills. Auras stay at 10 (PD2 uses 0; not tested here). Act 3 casters have default 0.
- Main attacks after balancing: Act 1 arrow 50, Act 2 Jab 70, Act 3 Fire Ball 60 / Glacial Spike 60 / Chain Lightning 65, Act 5 Might 10 + Whirlwind 70 (PD2 has 60 on its Whirlwind merc and spreads the rest over Battle Orders and Battle Cry).
- Skill ranks follow PD2's progression. Known differences: Act 3 masteries are 18 (PD2 27), Prayer is 21 (PD2 18), Chain Lightning and Glacial Spike are stock skills (PD2 uses custom merc versions). Battle Orders is deliberately not given to Act 5.
- Equalized across difficulty for the expansion rows (version 100): same stats and skill levels at the same merc level; only hire gold scales.
