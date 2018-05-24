# Game Commands

Common commands that can't be categorized as an "action" taken in combat.

**Heal** - `!heal 12` `!heal 2d8+2` `!heal`

This command will heal your character by the amount provided. It is nearly the same as `!g hp +12` but will not allow overhealing. If no string is provided it will just heal 1 hp.

**Hit Dice** - `!hitdice d6 1` `!hitdice 8 2` `!hitdice d12 4` `!hitdice`

This command will roll the specified hit die and heal you for that amount plus your CON modifier per die.
This command does require you to set up your level using `!level` beforehand. Custom counters will automatically be generated.

**HP Roll** - `!hproll wiz` `!hproll barb 2`

Rolls for your hp using the class you supply. Won't roll anything if you do not give it a class. Give it a number at the end to roll multiple levels.

**Level** - `!level fighter 3` `!level Wizard 12`

Sets character variables for use in the CWM aliases. Multiclass characters will need to call the command once for each class. Upon level up be sure to update your level using this command. DiceCloud users should not need to use this command.

**Restore Hit Die** - `!rhitdice d6 2` `!rhitdie 12 4`

This command restores your hit specified hit dice count by the amount given. Requires counters to be set up.

**Surprise** - `!surprise`

Prints the rules for the surprised condition.


# Action Commands

Specific actions that may be taken and require a skill check typically.

**Grapple** - `!grapple` `!grapple adv`

Performs an Athletics Grapple check.

**Overrun** - `!overrun` `!overrun adv`

Performs an Athletics Overrun check.

**Potion** - `!potion` `!potion greater` `!potion Supreme`

Drinks a potion and restores hp. Valid potions options are: Supreme, Superior, and Greater. Anything else will default to the lowest level potion.

**Prone** - `!prone` `!prone adv`

Performs an Athletics check to knock a target Prone.

**Push** - `!push` `!push adv`

Performs an Athletics check to shove a target.

**Battering Ram** - `!ram` `!ram adv`

Performs an Athletics check to break down a door with a portable battering ram. The +4 Strength bonus is already added.

**Scroll** - `!scroll 6` `!scroll 3 Fireball`

Performs an spellcasting ability check to cast a spell from a scroll or to copy it as a Wizard. If you supply a spell name (with "'s if there are spaces) it will also cast the spell if you succeed.

**Shove** - `!shove` `!shove adv`

Performs an Athletics check to shove a target.

**Tumble** - `!tumble` `!tumble adv`

Performs an Acrobatics Tumble check.

# Cantrips

## Cantrip Snippets
Many cantrips are done through snippets. See the Snippets description at the top folder level.
* Booming Blade
* Green Flame Blade
* Guidance
* Resistance

**Toll the Dead** - `!toll`

Casts the Toll the Dead spell and rolls for damage for both cases.

# Level 3 Spells

**Counterspell** - `!counterspell 5` `!counterspell 9`

Performs a spellcasting ability check to counter a spell of a certain level. If the spell slot used automatically cancels the other spell there is no need to run this alias.
