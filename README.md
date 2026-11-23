# Will Scarlet's Reformed for Diablo II

A Diablo II soft-mod (TXT files) that contains all my preferred changes to the game over the last 25 years.

![Cover Art](https://i.imgur.com/VEMcsYc.jpeg)

Intended for use w/ the [Diablo II PlugY QOL](https://github.com/whipowill/d2-plugy-qol) modpack.

## Introduction

When you've played a game for decades, you can get particular about how you like things to be.  This mod represents changes I've made over the years to enhance quality-of-life and boost what I felt were the fun and interesting aspects of the game.

## Features

- __Better Rune Drops__ - mid and high rune drop chance is linear instead of parabolic
- __Worldstone Shards__ - corrupt your items to add random sockets w/ a 50% chance it will fail
- __Melee Splash Damage__ - melee attacks deal 100% splash damage in a small radius
- __More Socketable Items__ - gloves, belts, boots, and throwing weapons are socketable
- __New Endgame Farming__ - keys drop from all Prime and Lesser Evils
- __Retrofit Endgame Materials__ - evil essences are now used as free crafting recipes
- __Class & Mob Bug Fixes__ - class bugs fixed, monster bugs fixed

## Install

- Copy and paste the ``Data`` folder into your Diablo II game directory.

## Changes

- Potions w/ duration last 5 minutes
- Items w/ stacks have increased size
- Shrine auras can stack on each other

### Worldstone Shards

A new item:

The __Worldstone Shard__ allows "corrupting" items to add random sockets.  This is a simple corrupting mechanic that allows you to make use of the various gems, jewels, and runes in the game to enhance your items.

Used in the Horadric Cube w/ any magic, rare, crafted, set, or unique item -- any equipable item other than jewelry, quivers, or charms.  There is a 50% chance the corruption will yield only a single socket.

### Weapons & Gear

- Melee weapons spawn w/ splash damage
- Magic and rare quivers are possible

Weapons now have increased ranges of attack:

- Stabbing Weapons (knives) - 1 (from 0)
- 1H Weapons (swords, axes, maces, claws) - 2 (from 1)
- 2H Weapons (swords, axes, maces, javelins) - 3 (from 2)
- Long Weapons (polearms, spears) - 4 (from 3)
- Ranged Weapons (bows, crossbows) - 0 (unchanged)

New socketable items:

- Gloves are socketable (up to 3 sockets)
- Belts are socketable (up to 2 sockets)
- Boots are socketable (up to 3 sockets)
- Throwing weapons are socketable (up to 3 sockets)

### Classes & Skills

- Barbarian
	- Leap, Shout, Battle Orders, Battle Command allowed in town
- Amazon
	- Dodge, Avoid, Evade bug fixed (per technique by [Nagahaku](https://d2mods.info/forum/viewtopic.php?p=500423&sid=923afb1f8828e76713d3c8a1f9f78ff1#p500423))
    - Impale replaced w/ Javelin Mastery
    - Jab and Fend synergies added
- Sorceress
	- Teleport allowed in town
	- Meteor lands 2/3 faster
    - Blizzard lands more evenly
	- All cooldowns reduced to 0.6 seconds
- Druid
	- Shapeshift lasts longer (1 min per point)
	- Beasts have increased critical chance (15% from 5%)
    - Beasts have Open Wounds on attack
    - Beasts have Splash Damage on attack
	- Spirits & vines cannot die
    - Teleport allowed in Shapeshift form

This mod makes a good faith effort to import most of the changes from D2R v2.4 with regard to slightly lower mana costs, slightly higher damage output, and some synergy tweaks.  Most of the work here was on making Summon Druid and Fendazon viable classes.

Also ``data/global/sfx/`` includes some files to mute/swap annoying sounds (Amazon and Sorceress).

### Mercenaries & Auras

All mercenaries have auras and some additional skills:

- Act 1
    - Fire - **Blessed Aim** / Fire Arrow / Exploding Arrow / Evade / Dodge
    - Ice - **Meditation** / Cold Arrow / Freezing Arrow / Evade / Dodge
- Act 2
    - Defensive - **Prayer** / Jab / Penetrate
    - Offensive - **Concentration** / Jab / Penetrate
- Act 3
    - Fire - **Cleansing** / Fire Ball / Meteor / Fire Mastery
    - Cold - **Prayer** / Glacial Spike / Blizzard / Cold Mastery
    - Lightning - **Meditation** / Chain Lightning / Charged Bolt / Lightning Mastery
- Act 5
    - All - **Might** / Whirlwind / Battle Orders

All mercenaries are the same no matter what difficulty you hire them (only the hire cost differs).

### Drops & Endgame

Adjustment of drop rates:

- Act bosses always drop quest loot
- Low quality gems become uncommon once you get to Act V in Normal
- Mid and high runes more likely (linear dropoff rather than parabolic)
- Nodrop rates are unchanged (still incentivized to use ``/players 8``)

Changes to who drops what:

- Countess always drops 3 runes
    - Normal up to Sol
    - Nightmare up to Ist
    - Hell up to Zod
- Prime & Lesser Evils drop uber keys (random keys, in all difficulties)
    - Andariel
    - Duriel
    - Mephisto
    - Diablo
    - Baal
- Prime Evils, Lesser Evils, and quest bosses drop evil essences (random essences, in all difficulties)
    - Blood Raven
    - Radament
    - Summoner
    - Travincal
    - Izual
    - Haphesto
    - Shenk
    - Nelethak

### Cube & Crafting

- Cube size is now 7x4 (credit [Sajon Oso](https://sajonoso.github.io/d2mods/))

Easier recipe formulas:

- Cube 2 runes -> 1 higher rank rune
- Cube 3 gems -> 1 higher rank gem
- Secret cow level only requires a Tome of Town Portal

Safe unsocket an item:

- Cube a stack of keys to release 1 key
- Cube a socketed item w/ a key and get the gems back

This one might be a big deal:

- Cube an ethereal item w/ an Uber Key to pull it from the ethereal realm (and vice versa)

Crafting changes:

- Hitpower crafting changed to greed (magic find + gold find)
- Evil essences now used as free craft recipes
    - Charged Essence of Hatred (yellow) - greed (magic find + gold find)
    - Festering Essence of Destruction (green) - safety
    - Twisted Essence of Suffering (blue) - caster
    - Burning Essence of Terror (red) - blood
- Use a perfect gem w/ an evil essence to change it's color
- Crafting recipes work on all magic items (no longer limited to particular [item codes](https://classic.battle.net/diablo2exp/items/crafteditems.shtml))
- Crafted weapons and armor can be upgraded as if they were rare

Rerolling charms changes:

- Use any charm with any essence to reroll

Basically, you can farm Travincal and accumulate free craft recipes.

Endgame changes:

- Only one key (any key) required to open red portal

### Areas & Rewards

More level 85 areas in Hell:

- Act 1
    - Tristram
    - Burial Grounds
    - Crypt
    - **Mausoleum** (no change)
    - Forgotten Tower
    - The Hole
    - **The Pit** (no change)
    - Catacombs
- Act 2
    - Stony Tomb
    - Halls of the Dead
    - Maggot Lair
    - **Ancient Tunnels** (no change)
    - Claw Viper Temple
    - Tal Rasha's Tomb
    - Tal Rasha's Chamber
- Act 3
    - Sewers
    - Swampy Pit
    - Flayer Dungeon
    - Ruined Temple
    - Disused Fane
    - Forgotten Reliquary
    - **Forgotten Temple** (no change)
    - **Ruined Fane** (no change)
    - **Disused Reliquary** (no change)
    - Durance of Hate
- Act 4
    - City of the Damned
    - **River of Flame** (no change)
    - **Chaos Sanctuary** (no change)
- Act 5
    - Infernal Pit
    - Pit of Acheron
    - Abaddon
    - Frozen River
    - Drifter Cavern
    - The Halls
    - **Worldstone Keep** (no change)
- Pandemonium
    - Sinking Sands
    - Matron's Den
    - Furnace of Pain
    - Uber Tristram

### Monsters & Bug Fixes

Fixed bugged monsters:

- [Bone Fetish](http://classic.battle.net/diablo2exp/monsters/act3-bonefetish.shtml) death explosion disabled
- [Tomb Viper](https://www.reddit.com/r/diablo2/comments/r7m6qm/tomb_vipers_a_history/) removed from the game

### Towns & Locations

- Deckard Cain now stands near chest in Act V

## External Links

- [Will Scarlet's PlugY QOL Modpack](https://github.com/whipowill/d2-plugy-qol) - a compilation of the best quality-of-life mods for the game