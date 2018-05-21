# Barbarian Commands

Contains commands used by Barbarians

## Game Commands

**rage** - `rage**`
Creates a custom counter and uses your current Barbarian level (according to `!level`) to modify it accordingly. Will print the rage description and number of rages available.
Note: If you view your Rage counter using !cc it is not the same as what is displayed when calling `!rage` due to the fact that counters can only scale linearly.

**brutal** - `!brutal` `!brutal d12` `!brutal 10`
Rolls damage for a Brutal Critical. Auto scales the number of dice. Defaults to a d10 weapon die.