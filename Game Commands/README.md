# Game Commands

Contains common commands used by all classes

## Actions folder

Contains a list of aliases a player can use as an action

## Game Commands

**heal** - `!heal 12` `!heal 2d8+2` `!heal`
This command will heal your character by the amount provided. It is nearly the same as `!g hp +12` but will not allow overhealing. If no string is provided it will just heal 1 hp.

**hitdice** - `!hitdice d6 1` `!hitdice 8 2` !hitdice d12 4`
This command will roll the specified hit die and heal you for that amount plus your CON modifier per die.
This command does require you either set up your level using `!level` or create the custom counters yourself (The counter name needs to be "Hit Die (d#)").
If you have use the !level command, the hitdie command should create the counters for you and use them.

**level** - `!level fighter 3` `!level Wizard 12`
Sets character variables for use in the CWM aliases. Multiclass characters will need to call the command once for each class. Upon level up be sure to update your level using this command.

**rhitdie** - `!rhitdice d6 2` `!rhitdie 12 4`
This command restores your hit specified hit dice count by the amount given.