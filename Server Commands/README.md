# Server Commands

These involve tools used for rules within the CWM Server

## The sgold Command
**sgold** - `!sgold` `!sgold Wizard` `!sgold barb 12` `!sgold 16` `!sgold 4 Monk`
	This command is used for rolling your starter gold for the server. Starting gold depends on what level tier you are rolling your character at but for new players it is always level 3, tier 1. If you don't supply a starting level then it will assume you are rolling at level 3.
	
	The command will also roll starting gold for if you choose to take no starting equipment. You just need to give it a class name.
	`!sgold class [tier] [class]`
	

## Other Server Commands

**alias_form** - `!alias_form`
    Prints the link to the suggestions form

**alias_list** - `!alias_list`
    Prints the link to the the documentation website on GitHub.

**convert** - `!convert 0 c` `!convert 12 mph` `!convert 70 f`
	This command takes in a number and a unit and converts it from metric to imperial and vice-versa.
	It is used with the !weather command to convert units.
	Will currently only convert between Celcius and Fahrenheit, or mph and jph.
	`!convert number (c | f | mph | kph)`

**newchar** - `!newchar`
    Rolls a new character just like the !randchar command. Prints out whether or not the stat line is valid. Uses the new rolling rolls from 28 May 2018.