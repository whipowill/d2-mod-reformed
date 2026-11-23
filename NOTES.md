# Notes

How each change in `Data/` works and where to edit it. Every path is relative to `Data/global/excel/` unless stated.

## Melee splash damage

Splash is an item property that fires a small missile at enemies around the target.

1. `Properties.txt`: property `splash` -> stat `item_splashonhit`.
2. `ItemStatCost.txt`: `item_splashonhit` -> description string `splashdamage` (in `patchstring.tbl`).
3. `AutoMagic.txt`: the affixes that carry it (Brute's = splash; Combo = splash + replenishing; the Harpoonist's / Spearmaiden's / Lancer's skill affixes also carry it). The property needs value `splash`, parameter `proc_SplashDamage` (or its id 371) and minimum `100`.
4. `Weapons.txt`, `UniqueItems.txt`, `SetItems.txt`: the `autoaffix` column points at those AutoMagic rows (ids 351-354). Leave them alone.
5. `Skills.txt`: skill `proc_SplashDamage` names the missile `proc_splashdamage` and how many to fire.
6. `Missiles.txt`: `proc_splashdamage`. `SrcDamage` is the damage share (128 = 100%, 64 = 50%); it is 128. `ToHit` is 0 so the splash always lands once the main hit connects (with a value of 1 the extra targets rolled at a lower attack rating than the main hit and missed often). `nextHit` stops a monster being hit twice in a moment.

Changes to the weapon table only reach newly spawned items.

## Worldstone Shard

- `Misc.txt`: last row `wss` (misc type, level 24, cost 24000, `invfile invwss`, `flippyfile flpgsr`, 1x1, gem-style `alternategfx gsw`, `component 16`, `namestr wss`). Always append new items at the end so no item index moves.
- `patchstring.tbl`: key `wss` = "Worldstone Shard".
- `TreasureClassEx.txt`: class `Orbs` lists `wss` as Item1.
- `CubeMain.txt`: the shard recipes use `wss`; the original cow-level recipe is kept.
- `Weapons.txt`: the six throwing potions are the original rows.
- `BH.cfg`: `ItemDisplay[wss]`.

**Never change what an existing item code is.** A saved item stores its code and a layout that depends on its table row; re-typing a code makes saved items unreadable (`Error Loading ... Error:14`) and no character loads. Add a new code instead.

## Weapon reach (`rangeadder` in `Weapons.txt`)

| weapons | rangeadder |
|---|---|
| daggers (`knif`), throwing knives and axes (`tkni`, `taxe`) | 1 |
| one-handed melee (swords, axes, maces, clubs, scepters, hammers, claws) | 2 |
| two-handed swings and javelins (`jave`, `ajav`) | 3 |
| spears (`spea`, `aspe`) and polearms (`pole`) | 4 |
| bows, crossbows, Amazon bows, wands, orbs | 0 (untouched) |

No existing value is lowered. It is read from the table at run time, so it also applies to saved items.

## Bows are destructible

`Weapons.txt` `nodurability` is cleared on every bow, Amazon bow and crossbow. An indestructible item cannot become ethereal, so the ethereal recipes did nothing on bows. Only newly generated bows get a durability bar.

## Ethereal cube recipes (`CubeMain.txt`)

- Make ethereal: 42 rows (armor or weapon, `noe`, `nos` or `sock=1..6`, Key of Terror / Hate / Destruction). Output `useitem,rem,reg,eth`, plus the property `ethereal` (min 1, max 1) in `mod 1` for unsocketed rows and `mod 2` for socketed rows (`mod 1` is the socket count).
- Make normal: the matching 42 rows with output `useitem,rem,reg,noe`.
- Rules learned: `useitem` only works in the output column; `eth` as an output only applies to a newly generated item, so existing items need the `ethereal` property; `useitem,mod,eth` rebuilds the item as a random base (a bow became a hatchet), so never use it; indestructible items cannot be ethereal; `noe` as an output does remove ethereal here.
- The five disabled "tempered" recipes were deleted.
- Column reference: Phrozen Keep, "Cubemain.txt Code Reference" and "Creating New Cube Recipes".

## Mercenaries (`Hireling.txt`)

- The hire screen only shows text for `HireDesc` 0-8 (strings 3371/3372, 11090/11088/11089, 3377/3376/3375). Labels are `Name (Aura)`; ids 3371, 3372 and 3375-3377 are in a loose `local/lng/eng/string.tbl`, 11088-11090 in `patchstring.tbl` (the Act 2 defensive text is key `PalMercExST1X`, "Jab (Prayer)").
- Act 2 has no "Combat" rows. Act 5 has Whirlwind in skill slot 2 and Battle Orders in slot 3 (it replaced Battle Cry; both use the same cast function, so only the name changes).
- Chances per row add up to 100: `DefaultChance` (plain attack) + aura 10 + skills. Act 3 casters have default 0.
- Top (Hell) level of each merc. Format: skill level, and in brackets the chance in percent that the merc picks it (a skill with no chance is a passive or a bonus only). The aura's chance is 10 for all; the rest of the 100 is the plain attack (`DefaultChance`).

| Merc | Aura (level) | Skills: level (chance %) | Plain attack |
|---|---|---|---|
| Act 1 fire | Blessed Aim 18 | Fire Arrow 22 (50), Exploding Arrow 22 (25), Dodge 5, Evade 5 | 15 |
| Act 1 cold | Meditation 18 | Cold Arrow 22 (50), Freezing Arrow 22 (25), Dodge 5, Evade 5 | 15 |
| Act 2 defense | Prayer 18 | Jab 24 (70), Penetrate 18 | 20 |
| Act 2 offense | Concentration 11 | Jab 24 (70), Penetrate 18 | 20 |
| Act 3 fire | Cleansing 30 | Fire Ball 20 (60), Meteor 19 (30), Fire Mastery 18 | 0 |
| Act 3 cold | Prayer 21 | Glacial Spike 18 (60), Blizzard 15 (30), Cold Mastery 18 | 0 |
| Act 3 lightning | Meditation 18 | Chain Lightning 22 (65), Charged Bolt 18 (25), Lightning Mastery 18 | 0 |
| Act 5 | Might 18 | Whirlwind 21 (60), Battle Orders 21 (15) | 15 |

- Concentration gives 60% + 15% per level and Might 40% + 10%, so the Act 2 offensive merc is set to aura level 1 / 6 / 11 (`Level1`, with `LvlPerLvl1` 5) to give +60 / +135 / +210%, equal to Might at the top. Concentration's interrupt protection is unchanged.
- Version 100 (expansion) rows equal version 0 at the same merc level; only hire gold scales.
- Act 5 Whirlwind: stock player Whirlwind (id 151) plus a custom sequence `seq_mercwhirlwind` in a loose `MonSeq.txt` (24 rows, the spin repeated three times), `Sk1lvl=18` on act5hire1/2, `Skill1=Whirlwind` in `MonStats.txt`. Its behaviour (starts in melee reach, travels through the pack) needs `qol.dll` (`[mercenary] whirlwind`).
- `States.txt`: the six `shrine_*` rows have the `curse` flag cleared.
- A wrong `.tbl` CRC crashes the game on load. Rebuild `.tbl` files with a writer that recomputes the CRC-16 (init 0xFFFF, over the data section).

## Amazon

- **Javelin and Spear Mastery** replaces Impale (same skill id and name, so Fend's prerequisite holds; required level 12). Only while wielding a spear. `Skills.txt` row `Impale`: `Param1` 44 and `Param2` 8 (attack rating 44% + 8% per level), `Param3` 28 and `Param4` 5 (damage 28% + 5%), `Param6` 35 (crit cap). These are the Barbarian spear mastery values. Passive damage adds to Enhanced Damage rather than multiplying it. Strings: four `patchstring.tbl` entries.
- **Jab:** `Param3` 0, `Param4` 5 (0% + 5% per level), `calc1` adds `skill('Fend') * par8` (par8 = 5).
- **Fend:** `Param3` 100, `Param4` 10 (100% + 10% per level), `calc2` adds `skill('Jab') * par8` (par8 = 10). Frame rollback `Param2` stays 60.
- **Guided Arrow** gets `Multiple Shot` levels at 12% (`calc1`, `Param8` 12); **Strafe** gets Guided Arrow at 10% and Multiple Shot at 5% per level (`calc2`).
- **Power, Charged and Lightning Strike:** the Lightning Fury synergy is removed; they share 14% (Lightning Strike 11%) among themselves.
- **Dodge, Avoid, Evade:** the bug fix uses three copies of the states (`dodge_fixed`, `avoid_fixed`, `evade_fixed`) that the skills point to (Nagahaku's method); the dodge animation no longer plays.

## Sorceress

- **Blizzard:** `Skills.txt` `Param3` (missile delay) 2 instead of 4, and `Missiles.txt` `blizzardcenter` `Range` 50 instead of 100: twice the shards per second for half as long. Keep `Range` at 100 for twice the total shards.
- **Meteor:** travel time 15-20 frames instead of 60.
- Nova and Thunder Storm gain a Static Field synergy; Blaze and Arctic Blast lose their dropped synergies.

## Druid

- **Beasts** (Spirit Wolf, Fenris, Grizzly, Raven): splash on 100% of hits; Open Wounds 100% on the wolf, Fenris and Grizzly; crit 15% on those three (stock 5%); the Raven keeps 5% and no Open Wounds. A monster only uses its `MonProp.txt` row through its own `MonProp` cell in `MonStats.txt`, so those cells must be filled for the wolves and bear.
- **Spirits and vines** (Oak Sage, Heart of Wolverine, Spirit of Barbs, Plague Poppy, Cycle of Life, Vines) are immune to every damage type and neutral so monsters ignore them. If the vines stop attacking, set their `Align` back to 1.
- **Shapeshift duration:** `Wearwolf`, `Wearbear` `auralencalc` is `1500 + skill('Shape Shifting')`, and `Shape Shifting` `Param1`/`Param2` are 1500/1500 (stock 1000/500).
- Teleport works while shapeshifted: `restrict` 1 lets a skill be used in any restricted state, and the wolf and bear forms are restricted states.
- Spirit Wolf's tooltip shows a cold damage line.

## Town, cooldowns, left mouse button

- Allowed in town: Teleport, Leap, Shout, Battle Orders, Battle Command (`Skills.txt` `InTown`).
- All 23 skills that have a cooldown use `delay` 15 frames (0.6 s at 25 fps).
- Every skill can go on the left mouse button (`leftskill`).
- Quiet-sound files for the Amazon and Sorceress are in `Data/global/sfx`.

## D2R skill port (patch 2.4 against stock 1.13c)

Class skills only: mana costs, damage numbers, damage-length and attack-rating values, synergy formulas with tooltip lines, durations and per-level percentages, and small behaviour items.

- **Mana:** Fire, Exploding, Immolation and Freezing Arrow, Blood and Fire Golem, War Cry, Nova, Inferno, Leap Attack.
- **Damage:** the `EMin`/`EMax` tables, `Param8` synergy percentages (Exploding Arrow 14, Inferno 16, Holy Fire 21, the sentries 11 to 18).
- **Synergies:** Raven gains the three animal summons (12%); Plague Poppy gains Rabies; Blade Sentinel, Blade Fury and Blade Shield gain each other; Berserk swaps Shout for Battle Orders; Leap Attack gains Leap; Holy Bolt, Fire Claws, Armageddon, Arctic Blast and the sentries lose the synergies D2R dropped. Edit the formula in `Skills.txt`, the percentage in its `ParamN`, and the tooltip lines in `SkillDesc.txt` (`dsc3line`). A formula using a blank `Param` adds nothing.
- **Parameters:** armor and Thunder Storm durations, Chilling Armor AC, masteries (Axe and Mace 40%, Pole Arm, Throwing and Spear 44%), Shout and Battle Command duration (Shout 750), Blood Golem damage, Whirlwind damage per attack (30% + 5% per level), Werebear bonuses, Maul, Fury's frame rollback (70), Dragon skills, Blade Shield and Venom durations, Energy Shield duration per level (600).
- **Small items:** Dragon Talon, Tail and Flight cannot be interrupted; Fist of the Heavens needs a target; Magic Arrow converts 5% + 2% per level to magic; Sacrifice's self-damage scales down with level; Leap's minimum distance is 8.
- **Thorns, Iron Golem, Barbs Aura:** keep the reflect percentage and add D2R's flat "attacker takes damage".
- **Leap Attack:** D2R's row plus its shockwave missile (physical, 10-20 at level 1 to about 150-300 at level 20, plus 10% per Leap level).
- **Held back on purpose:** `HitShift` on Inferno, Arctic Blast and Plague Poppy; the pet, golem and aura rewrites; D2R's cooldowns and tooltip wording; D2R-only skills.

## Splash on items

- Every unique (173 rows of `UniqueItems.txt`) and 19 set items (`SetItems.txt`) carry a splash property in the spare slot: `prop12` (sets `prop9`) = `splash`, `par` = `proc_SplashDamage`, `min` = 100, `max` = 1.
- Magic affixes: `MagicPrefix.txt` has "Brute's" and "Quartermaster's", `MagicSuffix.txt` "of the Brawler" and "of Renewal"; `AutoMagic.txt` has the six splash / replenishing / skill rows. `Weapons.txt` `auto prefix` (230 rows) points weapons at them.
- `ItemStatCost.txt` has the new stats `item_splashonhit` and `item_iscorrupted`; `Properties.txt` has `splash` and `corruption`.
- `MagicPrefix.txt`, `MagicSuffix.txt`, `RarePrefix.txt`, `RareSuffix.txt`: `itype` columns were extended so the affixes also roll on the newly socketable and quiver item types.

## Socketable gloves, belts, boots and throwing weapons

- `ItemTypes.txt`: `MaxSock1` / `MaxSock25` / `MaxSock40` = 2 / 2 / 3 for Boots, Gloves, Throwing Knife, Throwing Axe, Javelin and Amazon Javelin; Belt 2 / 2 / 2.
- `Armor.txt` (46 rows: gloves, belts, boots) and `Weapons.txt` (35 throwing rows): `hasinv` 1, `gemsockets` (3 for gloves, boots and throwing weapons; 2 for belts), `gemapplytype` 1.
- Magic and rare quivers: `ItemTypes.txt` Bow Quiver and Crossbow Quiver have `Normal` 0, `Rare` 1 and `Repair` 1.

## Stacks and potions

- `Misc.txt`: Town Portal and Identify books stack to 48 (stock 20), Skeleton Key to 24 (stock 12); Arrows min 120, spawn 240, max 480 and Bolts min 120, spawn 240, max 480, both with `auto prefix` 350 (Quartermaster's).
- Stamina, Antidote and Thawing potions last 300 seconds: `len` 7500 (stock 750).

## Horadric Cube

- `Inventory.txt` "Transmogrify Box Page 1" and "Transmogrify Box2": `gridX` 7 with new `gridLeft` / `gridRight` (60 / 263 and 140 / 343) make the cube 7 wide; the panel art is `global/ui/panel/supertransmogrifier.dc6`.
- `CubeMain.txt` (323 recipes; the magic-item reroll is the stock 3 perfect gems + 1 magic item; any one evil essence + 1 magic charm rerolls the charm, 4 recipes after it): 2 runes -> 1 higher rune (and the rune + gem variants), 3 gems -> 1 higher gem, keys (stack of N -> N-1 released), evil essence recipes (a perfect gem changes an essence's colour; essence + magic item = free craft), "hitpower" crafts changed to greed (magic find + gold find), a Town Portal tome alone opens the cow level (Wirt's Leg recipe kept), socketed-item + key returns the gems, Worldstone Shard corrupt recipes, throwing weapon protection recipes, one key opens the red portal, crafted items upgrade like rare ones, and the crafting recipes accept any magic item.

## Drops (`TreasureClassEx.txt`)

- New classes `Orbs` (holds `wss`), `Keys` (random uber keys) and `Essences` (random evil essences). The act bosses (Andariel, Duriel, Mephisto, Diablo, Baal) drop keys; those and the quest bosses (Blood Raven, Radament, Summoner, Travincal, Izual, Haphesto, Nelethak) drop essences, in all difficulties. Shenk the Overseer (`Siege Boss` in SuperUniques.txt) does too. His stock treasure class `Act 5 Super A` is shared with four other super uniques, so he has his own: `Shenk`, `Shenk (N)`, `Shenk (H)`, built like the other essence bosses (weighted, no helper class): picks 4 from `Act 5 Uitem A` 40 / `Act 5 Cpot A` 40 / `Essences` 4 (the stock class always gave 2 + 2; now the mix is random, about 18% of kills include an essence, the same as the other bosses). `SuperUniques.txt` is a copy of the stock file with only the Siege Boss TC columns changed.
- **Rule for adding essence (or other) drops to a monster:** put the existing `Essences` class directly in that monster's own drop list with a weight, as the other essence bosses do (it is probabilistic: a few percent per pick). Do not add helper classes (an earlier attempt, `Shenk Essences` with a NoDrop value, was rejected by the user) and do not give the monster an absolute drop. If the monster's stock class is shared with others, give it its own class plus a SuperUniques.txt / MonStats pointer, not a helper.
- `Runes 1` to `Runes 17`: mid and high runes use a linear drop-off instead of a parabolic one. The Countess always drops three runes (Normal up to Sol, Nightmare up to Ist, Hell up to Zod).
- `Act N Good` and `Citem` classes: act bosses always drop their quest loot; low-quality gems become uncommon from Act V Normal on.
- Nodrop rates are unchanged.

## Areas and monsters

- **Level 85 in Hell:** `Levels.txt` `MonLvl3Ex` is 85 on 60 rows (Tristram, Burial Grounds, Crypt, Forgotten Tower, The Hole, Catacombs, Stony Tomb, Halls of the Dead, Maggot Lair, Claw Viper Temple, Tal Rasha's Tomb and Chamber, the Sewers, Swampy Pit, Flayer Dungeon, Ruined Temple, Disused Fane, Forgotten Reliquary, Durance of Hate, City of the Damned, Infernal Pit, Pit of Acheron, Abaddon, Frozen River, Drifter Cavern, The Halls, Sinking Sands, Matron's Den, Furnace of Pain, Uber Tristram and their sub-levels). Areas that were already 85 are unchanged.
- **Bone Fetish:** `MonStats.txt` `deathDmg` cleared on all seven rows (no death explosion).
- **Tomb Viper:** `clawviper1` and `clawviper9` have `enabled` 0.
- **Diablo Clone:** `diabloclone` `Level` 45, `Level(N)` 75, `Drain` 50, `Drain(N)` 30 (stock 110 / 110 / 15 / 15).
- **Druid pets:** `PetType.txt` `group` cleared for the Spirit Wolf, Fenris and Grizzly; the vine's icons swapped (`micon1` vines, `micon2` cycleoflife); `MonProp.txt` new rows `spiritwolf`, `fenris`, `druidbear` carry Open Wounds.
- **Shrines:** `States.txt` `curse` cleared on the ten `shrine_*` rows (shrine effects no longer count as curses).
- **Town:** Deckard Cain stands near the chest in Act V (`global/tiles/expansion/town/townWest.ds1`).
- `MonStats2.txt` has 151 rows with edited animation-frame fields; they come from the Reformed base, not from this port.

## Strings (`local/lng/eng/patchstring.tbl`)

- Add new entries at the end so no earlier string index moves.
- `DiabloWalksEarth` is "Diablo walks the Earth..." (the Diablo Clone event in `qol.dll` uses it).
- Rebuild the file with the CRC recomputed (see Mercenaries).

## Looking things up

Table and field meanings: Phrozen Keep (d2mods.info) file guides.
- `Misc.txt`: the three uber organs (`mbr`, `dhn`, `bey`) use the same squishy `item_monsterguts` sound (drop and use, frame 14) as Khalim's organs, instead of `item_monsterbone`.
