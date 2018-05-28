## Alias Form
```GN
!servalias alias_form embed -title "Suggestions for server alias?" -desc "Tell us here: https://goo.gl/forms/tSsKgR8BbOpTbfMg2"
```

## Alias List
```GN
!servalias alias_list embed -title "List of server aliases and snippets:" -desc "https://github.com/nadizak/avrae_aliases"
```

## Convert
```GN
!servalias convert embed
{{set("inV", int("%1%") if "%1"+"%"!="%1%" else 0)}}
{{set("type", "%2%".lower())}}
{{set("error", type not in ["c", "f", "mph", "kph"])}}
{{set("out", (inV-32)*5/9 if type=="f" else (inV*9/5)+32 if type=="c" else inV*1.609344 if type=="mph" else inV*0.6213712 if type=="kph" else 0)}}
{{set("inUnit", "°F" if type=="f" else "°C" if type=="c" else type)}}
{{set("outUnit", "°C" if type=="f" else "°F" if type=="c" else "kph" if type=="mph" else "mph" if type=="kph" else '')}}
{{'''-title "Unsupported input"\n-desc "Accepted value and units are C (Celcius), F (Fahrenheit), mph, kph"''' if error else '''-title "$1 $2 is equal to roughly $3 $4"\n'''.replace('$1',str(inV)).replace('$2',inUnit).replace('$3',str(int(round(out,0)))).replace('$4',outUnit)}}
```

## New Character: 1@>15;1@>13
```GN
!servalias newchar embed
{{set("stats", [vroll("4d6kh3"), vroll("4d6kh3"), vroll("4d6kh3"), vroll("4d6kh3"), vroll("4d6kh3"), vroll("4d6kh3")])}}
{{set("statTotals", [stats[0].total, stats[1].total, stats[2].total, stats[3].total, stats[4].total, stats[5].total])}}
{{statTotals.sort()}}
{{set("valid", (statTotals[5] >= 15) and (statTotals[4] >= 13))}}
-desc "
`STR`: {{stats[0]}} {{'\:white_check_mark:' if stats[0].total>14 else '\:ballot_box_with_check:' if stats[0].total>12 else ''}}
`DEX`: {{stats[1]}} {{'\:white_check_mark:' if stats[1].total>14 else '\:ballot_box_with_check:' if stats[1].total>12 else ''}}
`CON`: {{stats[2]}} {{'\:white_check_mark:' if stats[2].total>14 else '\:ballot_box_with_check:' if stats[2].total>12 else ''}}
`INT`: {{stats[3]}} {{'\:white_check_mark:' if stats[3].total>14 else '\:ballot_box_with_check:' if stats[3].total>12 else ''}}
`WIS`: {{stats[4]}} {{'\:white_check_mark:' if stats[4].total>14 else '\:ballot_box_with_check:' if stats[4].total>12 else ''}}
`CHR`: {{stats[5]}} {{'\:white_check_mark:' if stats[5].total>14 else '\:ballot_box_with_check:' if stats[5].total>12 else ''}}"
-footer "{{'You may re-roll for another stat line because you do not have at least one 15+ stat with another stat at 13+' if not valid else 'This is a valid stat line. Re-roll until you have 2 valid stat lines and then choose one. Make sure an organizer approves your rolls.'}}"
```

## Starting Gold
```GN
!servalias sgold embed
{{set("clas", "%1%".capitalize())}}
{{set("classList", ["Barbarian", "Bard", "Cleric", "Druid", "Fighter", "Monk", "Paladin", "Ranger", "Rogue", "Sorcerer", "Warlock", "Wizard"])}}
{{set("index", classList.index(clas) if clas in classList else -1)}}
{{set("classRollList", ["2d4*10", "5d4*10", "5d4*10", "2d4*10", "5d4*10", "5d4", "5d4*10", "5d4*10", "4d4*10", "3d4*10", "4d4*10", "4d4*10"])}}
{{set("classRoll", classRollList[index] if index >=0 else "0")}}
{{set("level", int("%2%") if "%2%"!="%"+"2%" else 0)}}
{{set("tier", 4 if level>15 else 3 if level>11 else 2 if level>7 else 1 if level>3 else 0)}}
{{set("tierRolls", ["1d4*10", "100+1d4*10", "1000+1d10*100", "5000+1d10*250", "10000+1d10*500"])}}
{{set("tierRoll", tierRolls[tier] if tier >=0 and tier <5 else "0")}}

{{set("classgold", vroll(classRoll))}}
{{set("servergold", vroll(tierRoll))}}

{{'''-title "Rolling gold for $0!"\n-desc "**Starting Equipment**\nWhen you create your character, you receive equipment based on a combination of your class and background. Alternatively, you can start with a number of gold pieces based on your class and spend them on items listed in the Player's Handbook."\n-f "Starting gold for Tier $3 | $1"\n-f "Additional $0 starting gold if no starting equipment. | $2"'''.replace('$0', clas).replace('$1', str(servergold)).replace('$2', str(classgold)).replace('$3', str(tier+1)) if index >=0 else '''-title "sgold Command Usage"\n-desc "Please use the command by typing **!sgold class** (e.g. !sgold Monk) to roll for starting gold.\n\nYou may also use **!sgold class level** (e.g. !sgold Druid 12) to roll for starting gold at a different starting level.\nStarting levels are dictated in the CWM guide.\n"'''}}
-footer "Starting Equipment | PHB 143"
```
