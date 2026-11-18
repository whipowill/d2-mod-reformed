# Reformed for Diablo II

A Diablo II soft-mod (TXT files) that contains all my preferred changes to the game over the last 25 years.

Intended for use w/ the [Diablo II PlugY QOL](https://github.com/whipowill/d2-plugy-qol) modpack.

## Introduction

When you've played a game for decades, you can get particular about how you like things to be.  This mod represents all the changes I've made over the years to enhance quality-of-life and boost what I felt were the fun and interesting aspects of the game.  Minor changes all, nothing too much.

My goal is to provide these changes for both **D2LOD (v1.13d)** and **D2R (v2.4)**.  Sadly, even w/ mod parity between the games, you can't transfer a character from one to the other.  For whatever reason it just doesn't work.  I assume it has something to do w/ the internal D2R file encoding that assumes vanilla stats on items.

The D2LOD version of this mod is the best version, and the D2R port is close but not always up to date.  Because I pretty much only play D2LOD, that's the version that gets the most love.  You can check the TODO file to see what those not-yet-ported changes might be.  It's a labor of love, and I will get to it when I can.

## Features

I hope you'll find these changes tasteful while still maintaining the spirit of original Diablo II.  The idea is to make minor improvements w/out changing things so much that it becomes an entirely different game.

- __Better Rune Drops__ - mid and high rune drop chance is linear instead of parabolic
- __Worldstone Shards__ - corrupt your items to add random sockets w/ a 50% chance it will fail
- __Melee Splash Damage__ - melee attacks deal 50% splash damage in a small radius
- __Infinite Ammunition__ - quivers and throw weapons spawn w/ replenishing quantity
- __More Socketable Items__ - gloves, belts, boots, and throwing weapons are socketable
- __New Endgame Farming__ - keys drop from all Prime and Lesser Evils
- __Retrofit Endgame Materials__ - evil essences are now used as free crafting recipes
- __Class & Mob Bug Fixes__ - class bugs fixed, monster bugs fixed

## Install

**D2LOD**

- Merge the contents of the ``D2LOD`` folder into your Diablo II game directory.

**D2R**

- Merge the contents of the ``D2R`` folder into your Diablo II game directory.

## Changes

For a precise view of the game changes enacted here, you can check out my [TXT change repo](https://github.com/whipowill/d2-113c-txt-changes) which highlights exactly what I've done.

### Items & Mechanics

Minor QOL tweaks:

- Potions w/ duration last 5 minutes
- Items w/ stacks have increased size
- Shines auras can stack on each other

Important mechanics changes:

- Melee weapons spawn w/ splash damage (50% weapon damage at short range)
- Projectile weapons spawn w/ replenishing quantity
- Magic and rare quivers are possible

New socketable items:

- Gloves are socketable (up to 3 sockets)
- Belts are socketable (up to 2 sockets)
- Boots are socketable (up to 3 sockets)
- Throwing weapons are socketable (up to 3 sockets)

A new item:

The __Worldstone Shard__ allows "corrupting" items to add random sockets.  This is a simple corrupting mechanic that allows you to make use of the various gems, jewels, and runes in the game to enhance your items.

Used in the Horadric Cube w/ any magic, rare, crafted, set, or unique item -- any equipable item other than jewelry, quivers, or charms.  There is a 50% chance the corruption will yield only a single socket.

### Weapons & Gear

Weapons now fall into these categories w/ increased ranges of attack:

- Stabbing Weapons (knives) - 1 (default 0)
- 1H Weapons (swords, axes, maces, claws) - 2 (default 1)
- 2H Weapons (swords, axes, maces, javelins) - 3 (default 2)
- Long Weapons (polearms, spears) - 4 (default 3)
- Ranged Weapons (bows, crossbows) - 0 (default 0)

Extends the range of weapons over the vanilla game a tad.

### Classes & Skills

- Barbarian
	- Leap, Shout, Battle Orders, Battle Command allowed in town
- Amazon
	- Dodge, Avoid, Evade bug fixed (per technique by [Nagahaku](https://d2mods.info/forum/viewtopic.php?p=500423&sid=923afb1f8828e76713d3c8a1f9f78ff1#p500423))
- Sorceress
	- Teleport allowed in town
	- Meteor lands 2/3 faster
	- All cooldowns reduced to 0.5 seconds
- Druid
	- Shapeshift lasts longer (1 min/point)
    - Spirit Wolves now do cold instead of physical damage (like D2R)
	- All beasts can be summoned at same time (like D2R)
	- All beasts have increased critical chance (15% from 5%)
    - All beasts apply Open Wounds on attack (makes sense, right?)
	- Spirits & vines cannot die (like PD2)
	- Teleport allowed in shapeshift form

Also ``data/global/sfx/`` includes some files to mute/swap annoying sounds (Amazon and Sorceress).

### Drops & Endgame

Adjustment of drop rates:

- Act bosses always drop quest loot
- Low quality gems become uncommon once you get to Act V in Normal
- Mid and high runes more likely (linear dropoff rather than parabolic)
- Nodrop rates are unchanged (still incentivized to ``/players 8``)

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
    - Nelethak

I wanted to incentivize doing full game runs (instead of just farming a single boss in a hard-to-access area like Arcane Santuary).  This way you can start a run and find a good reason to do the whole game, quest bosses and act bosses.  As you'll see in the next category, evil essences now serve a purpose in a PlugY world by being used as free crafting recipes.

### Cube & Crafting

Help w/ limited inventory space:

- Cube size is now 7x4 (credit [Sajon Oso](https://sajonoso.github.io/d2mods/))

Stackable items (D2R only, this change is not in D2LOD):

- Gems are stackable by converting in cube
- Jewels are stackable by converting in cube
- Runes are stackable by converting in cube

The problem w/ this in D2R is that you can't control-click stackable items into your stash.  You have to pickup the stack in your stash, move it to your inventory, add the new item to the stack, then move it back.

Minor QOL tweaks:

- Cube 2 runes -> 1 higher rank rune
- Cube 3 gems -> 1 higher rank gem
- Secret cow level only requires a Tome of Town Portal

This one might be a big deal:

- Cube an ethereal item w/ an Uber Key to pull it from the ethereal realm (and vice versa)

Safe unsocket:

- Cube a stack of keys to release 1 key
- Cube a socketed item w/ a key and get the gems back

Crafting changes:

- Hitpower crafting changed to greed (magic find + gold find)
- Evil essences now used for crafting (free craft recipes)
    - Twisted Essence of Suffering (blue) - greed (used to be hitpower)
    - Charged Essence of Hatred (yellow) - caster
    - Burning Essence of Terror (red) - blood
    - Festering Essence of Destruction (green) - safety
- Use a perfect gem w/ an evil essence to change it's color
- Crafting recipes work on all magic items (no longer limited to particular [item codes](https://classic.battle.net/diablo2exp/items/crafteditems.shtml))
- Crafted weapons and armor can be upgraded as if they were rare
- Token of Absolution removed from the game

Basically, you can farm Travincal and accumulate a ton of free craft recipes.

Endgame changes:

- Only one key (any key) required to open red portal (still debating this one)

### Mercenaries & Auras

All mercenaries have auras and some additional skills:

- Act 1
	- Fire - **Blessed Aim** / Fire Arrow / Exploding Arrow / Evade / Dodge
	- Ice - **Meditation** / Cold Arrow / Freezing Arrow / Evade / Dodge
- Act 2
	- Defense - **Defiance** / Jab / Penetrate
	- Offense - **Concentration** / Jab / Penetrate
- Act 3
	- Fire - **Cleansing** / Fire Ball / Meteor / Fire Mastery
	- Cold - **Prayer** / Glacial Spike / Blizzard / Cold Mastery
	- Lightning - **Meditation** / Chain Lightning / Charged Bolt / Lightning Mastery
- Act 5
	- All - **Might** / Whirlwind (needs `qol.dll` to behave properly)

Also, all mercenaries are the same no matter what difficulty you hire them (only the hire cost differs).

Skill choice chances for every mercenary add up to 100 (default attack + aura 10 + skills).

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

As mentioned previously, the idea is to incentivize full game runs w/ forays into the off-the-beaten-path areas.  This gives you a reason to take that door to an area you would normally skip.

### Monsters & Bug Fixes

Fixed bugged monsters:

- [Bone Fetish](http://classic.battle.net/diablo2exp/monsters/act3-bonefetish.shtml) death explosion disabled
- [Tomb Viper](https://www.reddit.com/r/diablo2/comments/r7m6qm/tomb_vipers_a_history/) removed from the game

### Towns & Locations

- Deckard Cain now stands near chest in Act V

## External Links

- [Will Scarlet's PlugY QOL Modpack](https://github.com/whipowill/d2-plugy-qol) - a compilation of the best quality-of-life mods for the game