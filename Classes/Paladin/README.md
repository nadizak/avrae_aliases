# Paladin Commands

Common commands used by Paladins that will auto create and update counters and roll dice for you.
Most aliases will require `!level` to be set up correctly beforehand.

**Divine Sense** - `!divinesense`

Uses the Divine Sense ability. Creates and modifies counters for the ability.

**Lay on Hands** - `!layonhands me 20` `!layonhands 20 self` `!layonhands me 30`

Uses the Lay on Hands ability to heal yourself or a target. If "me" or "self" is in the arguments it will restore your own HP automatically. Will create a self-updating counter if it doesn't already exist.

**Divine Smite** - `!smite 1` `!smite crit 3` `!smite 2 critical`

Uses the Divine Smite ability. Must pass a spell slot level or it will assume first level slot. If crit is passed it will double the dice rolled. Will decrement your spell slot as well.

**Channel Divinity** - `!channel`

Uses the Channel Divinity ability. Creates and modifies counters for the ability. Currently does not do anything specific to the paladin subclass.

**Paladin Auras** - `!pld_aura`

Prints out the effects of your paladin aura. Currently does not do anything for any paladin subclass auras.