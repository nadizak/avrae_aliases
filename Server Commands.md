## CWM Search
```GN
!servalias cwm embed
{{output,key=load_json(get_gvar("b1f652c5-221d-4f2e-97a5-6adc595d9b50")[1:]),".."}}
{{data=output.data}}
{{query="&*&".split(" ")}}
{{[set("output",(output[key] if (q.lower() in output and not set("key", q.lower())) or ([set("key", k) for k in output.keys() if q and q.lower().replace(" ", "") in k.lower().replace(" ", "")]) else output)) for q in query]}}
{{query=" ".join([q for q in query if "&" not in q])}}
{{type=output.type if "type" in output else ""}}
{{list=[key for key in output.keys() if key not in data.a] if "list" in type else 0}}
{{list.sort() if list and ("sort" not in output or "none" not in output.sort) else 0}}
{{timeout="" if "notime" in query else output.t if "t" in output else "10" if list else ""}}
{{snippetEx="\n".join(output.snippetEx) if "snippetEx" in output else ""}}
{{aliasEx="\n".join(output.aliasEx) if "aliasEx" in output else ""}}
-title "{{output.title if "title" in output else "" if type == "bare" else f"!cwm {query}"}}"
-desc "{{output.desc if "desc" in output else "\n".join(list) if list else ""}}"
-footer "{{output.footer if "footer" in output else data.f if list else data.s if ("<" in snippetEx or "[" in snippetEx+aliasEx) else ""}}"
-thumb "{{"" if type == "bare" else output.thumb if "thumb" in output else data.t}}"
-image "{{"" if "image" not in output else output.image}}"
{{f'-t {timeout}' if timeout else ''}}
{{f'-f "Snippet Usage | {snippetEx}"' if snippetEx else ""}}
{{f'-f "Alias Usage | {aliasEx}"' if aliasEx else ""}}
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

## New Character
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
-footer "{{'You may re-roll for another stat line because you do not have at least one 15+ stat with another stat at 13+' if not valid else 'This is a valid stat line. Re-roll until you have 2 valid stat lines and then choose one. Make sure a helper approves your rolls.'}}"
```

## Starting Gold
```GN
!servalias sgold embed
{{classList=load_json(get_gvar("6bbbd645-9002-41af-9915-0948a2e7ec6c"))}}
{{classRollList=load_json(get_gvar("b1fa8f4a-41a5-4085-a4e4-58a3513e4690"))}}
{{tierRolls=load_json(get_gvar("75a8dd6b-4d91-45c6-9790-5293e25738cf"))}}
{{args="%1%%2%%3%%"}}
{{args=args[:args.index('%')]}}
{{clas=''.join([i for i in args if i.isalpha()])[:4].capitalize()}}
{{lvl=''.join([i for i in args if i.isdigit()])}}
{{lvl=int(lvl) if lvl else 3}}
{{clas=[i for i in classList if clas in i][0] if clas else ""}}
{{index=classList.index(clas) if clas in classList else -1}}
{{classRoll=classRollList[index] if index >=0 else "0"}}
{{tier=4 if lvl>15 else 3 if lvl>11 else 2 if lvl>7 else 1 if lvl>3 else 0}}
{{tierRoll=tierRolls[tier] if tier >=0 and tier <5 else "0"}}
{{classgold=vroll(classRoll)}}
{{servergold=vroll(tierRoll)}}
-title "Rolling Starting Wealth{{f" For {clas}" if clas else ""}}!"
-desc "**Starting Equipment**
When you create your character, you receive **starting equipment** based on a combination of your **class** and **background** as listed in the PHB. Everyone also receives **additional gold** depending on their starting level. 

Instead of **starting equipment**, you can start with a number of gold pieces based on your class and spend them on items listed in the Player's Handbook. (Add your class to the sgold command to do this, e.g. `!sgold barb` or `!sgold Druid`)

You can also roll for a higher CWM level tier as per the player guide. (Add the level you are starting at to the command to do this, e.g. `!sgold 12`, `!sgold 16 Wiz`, or `!sgold monk 12`)"
{{f"-f \"Starting Gold for Level {lvl} (Tier {tier+1}) | {servergold}\""}}
{{f"-f \"Additional {clas} starting gold if no starting equipment. | {classgold}\"" if clas else ""}}
-footer "Starting Equipment | PHB 143"
```
