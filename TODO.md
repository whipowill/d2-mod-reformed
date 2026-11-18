# Changes Needed on D2R

This are my notes on features I've added to D2LOD that need to be ported to D2R.

## Not Yet Ported

Amazon bug fix (Dodge/Avoid/Evade, even needed in D2R? check in game first):

- ``Skills.txt`` ``passivestate`` -> ``dodge_fixed`` / ``avoid_fixed`` / ``evade_fixed``, plus the three matching extra rows at the end of ``States.txt`` (D2R mod has no ``states.txt`` yet)

## Ported

- ``Cubemain.txt``
- Splash damage and corruption stuff
- Prefix and suffix files (magic quiver stuff)
- ``Treasureclassex.txt`` (drop, shard, essence, etc changes)
- ``Skills.txt`` (cooldown changes)
- ``Missiles.txt`` (meteor stuff)
- New socketable items
- Lvl 85 zones

## Ported 2026-11-17

- ``Weapons.txt`` - ``rangeadder`` rules (201 of 231 weapons raised, same as D2LOD)
- ``Monstats.txt`` - Tomb Viper (``clawviper1``, ``clawviper9``) disabled, Bone Fetish death explosion (``deathDmg``) cleared
- ``Monstats2.txt`` - ``isAtt`` cleared on the three Druid spirits (new file, copied from D2R stock)
- ``Cubemain.txt`` - Token of Absolution recipes removed; cow level: tome-only recipe relabelled, original Wirt's Leg + tome recipe added
- Worldstone Shard needed no port: D2R already has it as its own item ``wsh`` (not a re-typed potion), ``Orbs`` drops it and the gas/oil potions are still stock
- ``States.txt`` (new ``states.txt``) - ``curse`` flag cleared on the ten ``shrine_*`` rows so shrines stack (D2LOD NOTES said six, it is ten)
- ``Hireling.txt`` - rebuilt from D2R stock with the D2LOD design: auras and skills as in D2LOD (Act 2 Combat merc removed, Defense = Defiance, Offense = Concentration), skill chances add up to 100, Normal stats copied to Nightmare and Hell at the same level (hire gold unchanged), Act 5 = Might + Whirlwind. D2R keeps its own stat numbers, so values differ from D2LOD. The D2R-only Frenzy merc (class 560) is untouched
- ``Monstats.txt`` - ``act5hire2`` gets Whirlwind (``seq_ancientwhirlwind``, level 15). Without ``qol.dll`` the spin behaves like stock Whirlwind, untested in D2R
- ``ui.json`` (copied from D2R stock, five strings edited) - hire labels now show the aura, e.g. "Fire Arrow (Blessed Aim)"
