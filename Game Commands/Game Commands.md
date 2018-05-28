## Heal
```GN
!servalias heal embed
{{set("input", "%1%" if "%1"+"%"!="%1%" else "1")}}
{{set("heal", vroll(input))}}
{{set_hp(min(hp, heal.total + currentHp))}}
-title "<name> regains HP!"
-desc "You are healed for {{input}} hit points."
-f "Hit Points|{{get_hp()}} / {{hp}}"
-f "Healing Done|{{str(heal)}}"
-thumb <image>
-color <color>
```

## Hit Dice
```GN
!servalias hitdice embed
{{set("d12", int(Barbarian))}}
{{set("d10", int(Fighter) + int(Paladin) + int(Ranger))}}
{{set("d8", int(Bard) + int(Cleric) + int(Druid) + int(Monk) + int(Rogue) + int(Warlock))}}
{{set("d6", int(Sorcerer) + int(Wizard))}}
{{create_cc_nx("Hit Dice (d12)", 0, "Barbarian") if d12 else 0}}
{{create_cc_nx("Hit Dice (d10)", 0, "Fighter+Paladin+Ranger") if d10 else 0}}
{{create_cc_nx("Hit Dice (d8)", 0, "Bard+Cleric+Druid+Monk+Rogue+Warlock") if d8 else 0}}
{{create_cc_nx("Hit Dice (d6)", 0, "Sorcerer+Wizard") if d6 else 0}}
{{set('die', '' if "%1"+"%"=="%1%" else 'd%1%' if '%1%'[0] != 'd' else '%1%')}}
{{set('used', '%2%' if '%2'+'%'!='%2%' else '1')}}
{{set('dieStr', "Hit Dice (" + die + ")")}}
{{mod_cc(dieStr, -1*int(used), True) if die else 0}}
{{set("heal", vroll(used+die+"+"+str(constitutionMod*int(used))))}}
{{set_hp(min(hp, heal.total + currentHp)) if die else 0}}
-title "{{(name + 'takes a Short Rest!') if die else 'Hit Dice'}}" 
-desc "{{get_gvar("8e7251ab-1596-48b0-976d-fdc1ecbbab94")}}"
{{('-f "Healing Received|' + str(heal) + '"') if die else ''}} 
{{('-f "Hit Points|' + str(get_hp()) + ' / ' + str(hp) + '"') if die else ''}} 
{{('-f "Hit Dice (d6)|' + str(get_cc("Hit Dice (d6)")) + ' / ' + str(get_cc_max("Hit Dice (d6)")) + '"') if d6 else ''}}
{{('-f "Hit Dice (d8)|' + str(get_cc("Hit Dice (d8)")) + ' / ' + str(get_cc_max("Hit Dice (d8)")) + '"') if d8 else ''}} 
{{('-f "Hit Dice (d10)|' + str(get_cc("Hit Dice (d10)")) + ' / ' + str(get_cc_max("Hit Dice (d10)")) + '"') if d10 else ''}} 
{{('-f "Hit Dice (d12)|' + str(get_cc("Hit Dice (d12)")) + ' / ' + str(get_cc_max("Hit Dice (d12)")) + '"') if d12 else ''}}
-footer "Adventuring | PHB 186" 
-color <color> -thumb <image>
```

## HP Roll (For level up hp)
```GN
!servalias hproll embed
{{set("dice", "%2%" if "%2"+"%"!="%2%" else "1")}}
{{set("clas", "%1%".lower())}}
{{set("dieSize", 6 if clas in "wizard|sorcerer" else 8 if clas in "artificer|bard|cleric|druid|monk|rogue|warlock" else 10 if clas in "fighter|paladin|ranger" else 12 if clas in "barbarian" else 0)}}
-title "Rolling for Hit Points{{'' if dice=="1" else (' for '+str(dice)+' levels')}}!"
-desc "The fact that you are using this means that you are daring enough to be using the intense method of **ROLLING** for your hit points! If you did use this and nothing appears, please be sure to use the format below:

`!hproll (class) (optional number of levels)`
E.g.: `!hproll barbarian` or `!hproll monk 2` for 2 levels"
{{('-f "Hit Points Roll | ' + str(vroll(dice+"d"+str(dieSize)+"+"+str(constitutionMod))) + '"') if dieSize else ''}}
-color <color> -thumb <image>
```

## Level Set
```GN
!servalias level embed
{{set("z","0")}}
{{set("clas","%1%".capitalize())}}
{{set("newLevel",int("%2%") if "%2"+"%"!="%2%" else 0)}}
{{set("classList",["Barbarian","Bard","Cleric","Druid","Fighter","Epic","Monk","Paladin","Ranger","Rogue","Sorcerer","Warlock","Wizard"])}}
{{set("error",clas not in classList or newLevel>20 or newLevel<0)}}
{{set_cvar_nx("Barbarian",0)}}
{{set_cvar_nx("Bard",0)}}
{{set_cvar_nx("Cleric",0)}}
{{set_cvar_nx("Druid",0)}}
{{set_cvar_nx("Fighter",0)}}
{{set_cvar_nx("Epic",0)}}
{{set_cvar_nx("Monk",0)}}
{{set_cvar_nx("Paladin",0)}}
{{set_cvar_nx("Ranger",0)}}
{{set_cvar_nx("Rogue",0)}}
{{set_cvar_nx("Sorcerer",0)}}
{{set_cvar_nx("Warlock",0)}}
{{set_cvar_nx("Wizard",0)}}
{{error or set_cvar(clas,newLevel)}}

-title "<name> Level Summary for <name>"
-f "Character Level | {{level}}"
-f "Class Levels | {{('Barbarian: '+str(Barbarian)+"\n") if Barbarian!=z else ''}}{{('Bard: '+str(Bard)+"\n") if Bard!=z else ''}}{{('Cleric: '+str(Cleric)+"\n") if Cleric!=z else ''}}{{('Druid: '+str(Druid)+"\n") if Druid!=z else ''}}{{('Fighter: '+str(Fighter)+"\n") if Fighter!=z else ''}}{{('Epic Levels: '+str(Epic)+"\n") if Epic!=z else ''}}{{('Monk: '+str(Monk)+"\n") if Monk!=z else ''}}{{('Paladin: '+str(Paladin)+"\n") if Paladin!=z else ''}}{{('Ranger: '+str(Ranger)+"\n") if Ranger!=z else ''}}{{('Rogue: '+str(Rogue)+"\n") if Rogue!=z else ''}}{{('Sorcerer: '+str(Sorcerer)+"\n") if Sorcerer!=z else ''}}{{('Warlock: '+str(Warlock)+"\n") if Warlock!=z else ''}}{{('Wizard: '+str(Wizard)+"\n") if Wizard!=z else ''}}{{"" if (int(Barbarian)+int(Bard)+int(Cleric)+int(Druid)+int(Fighter)+int(Monk)+int(Paladin)+int(Ranger)+int(Rogue)+int(Sorcerer)+int(Warlock)+int(Wizard)) else "None"}}"
-color <color>
-thumb "<image>"
-footer "If Sum of class levels does not equal character level, you need to run `!level class #`"
```

## Restore Hit Die
```GN
!servalias rhitdie embed
{{set('die', '%1%' if '%1'+'%'!='%1%' else 'd')}}
{{set('dieStr', "Hit Dice (" + ('d'+die if die[0]!='d' else die) + ")")}}
{{set('dieDelta', '%2%' if '%2'+'%'!='%2%' else 0)}}
{{set('error', die == 'd')}}
{{error or mod_cc(dieStr, int(dieDelta))}}
{{set('currentDie', 0 if error else get_cc(dieStr))}}
{{set('maxDie', 0 if error else get_cc_max(dieStr))}}

{{'''-title "<name> regains spent Hit Dice!" \n-desc "At the end of a long rest, you regain spent Hit Dice, up to a number of dice equal to half your total number of them." \n-f "$d|$c / $m"\n-footer "Adventuring | PHB 186" \n-thumb "<image>"\n-color "<color>"\n'''.replace('$d', dieStr).replace('$c', str(currentDie)).replace('$m', str(maxDie)) if not error else '''-title "Incorrect usage of *rhitdie*"\n-desc "\n**Examples of correct usage:**\n!rhitdie d6 +1\n!rhitdie d8 2\n!rhitdie d8\n!rhitdie d12 -2\n!rhitdie 10 +3"'''}}
```

## Surprise Rules
```GN
!servalias surprise embed
-title "Surprise Rounds"
-desc "If you’re surprised, you can’t move or take an action on your first turn of the combat, and you can’t take a reaction until that turn ends. A member of a group can be surprised even if the other members aren’t."
-footer "PHB 189"
```
