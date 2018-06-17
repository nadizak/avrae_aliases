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
{{('-f "Hit Points Roll | ' + str(vroll(dice+"d"+str(dieSize))) + '"') if dieSize else ''}}
{{f"-f \"Constitution | Don't forget to add you CON modifier * {dice}\""}}
-color <color> -thumb <image>
```

## Level Set
```GN
!servalias level embed
{{classList=load_json(get_gvar("6bbbd645-9002-41af-9915-0948a2e7ec6c"))}}
{{set("z","0")}}
{{clas="%1%"[:4].capitalize()}}
{{clas=[i for i in classList if clas in i]}}
{{clas=clas[0] if len(clas) else ""}}
{{set("newLevel",int("%2%") if "%2"+"%"!="%2%" else 0)}}
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

## Money
**Credit to @silverbass#2407**
```GN
!servalias money embed 
{{set_cvar("money",0) if not exists("money") else ""}}
{{set("value","reset" if "%1%" in "reset" else "help" if "%1%" in "help" else 0 if "%1%" == "%1"+"%" or not ("%1%".lstrip("-+").isdigit() or "%1%" in "+-") else int("%1%%2%") if "%1%" in "+-" and "%2%"!="%2"+"%" else int("%1%"))}}
{{set("coin", "gp" if ("%2%" == "%2"+"%" and  not "%1%" in "+-") or ("%3%" == "%3"+"%" and "%1%" in "+-") else "%2%"  if not "%1%" in "+-" else "%3%")}}
{{set("coin", coin.lower())}}
{{set("mult", .1 if coin in "sp" else 0.01 if coin in "cp" else 10 if coin in "pp" else 0.5 if coin in "ep" else 1)}} 
{{(set("value", -min(float(money), -mult*value)) or set("t",True)) if str(value) not in "help reset" and value<0 and (-mult*value)>float(money) else ""}}
{{set("coin","gp") if not str(value) in "help reset" and -value==round(float(money),2) else ""}}
{{set("mult", .1 if coin in "sp" else 0.01 if coin in "cp" else 10 if coin in "pp" else 0.5 if coin in "ep" else 1)}} 
{{(set_cvar('money',0) or set('value', 0)) if str(value) in "reset" else "" if str(value) in "help" else set_cvar('money',(float(money) + mult*value))}}
-title "{{"How To Use Money" if str(value) in "help" else name+" earns "+f"{int(value):,}"+" "+coin if value>0 else name+" spends "+f"{-value:,}"+" "+coin if value<0 else name+" has :moneybag: "+f"{round(float(money),2):,}"+" "+coin}}!" {{" -footer \"!money help for more info\"" if value==0 else "-f \"Total | :moneybag: "+f"{round(float(money),2):,}"+" gp\" -footer \"!money help for more info\"" if value!="help" else "-desc \"__"+" "*200+"__\" "+get_gvar("d0f8e956-280c-4187-a5cb-f542e7cba560")}} -color <color>
```

## Inventory
**Credit to @silverbass#2407**
```GN
!servalias inv embed {{set("x","&2&" if "%2%"!="%2"+"%" else "")}}{{set("m","%1%")}}{{set("m","h" if m in "help" else "r" if m in "delete" else "p" if x=="" else m if m=="+" or m=="-" or m=="?" else "p")}}{{set("n",int("%3%") if "%3%".isdigit() else 1)}}{{set("n",int(m+str(n)) if m in "+-" else 0)}}{{set_cvar("inv","") if m=="r" or not exists("inv") else ""}}{{set("m","p" if m=="r" else m)}}{{set("f",inv.lower().find(x.lower()) if x!="" else -1)}}{{set("f",-1 if f<0 else 0 if f==0 else f if inv[f]=="$" else inv.rfind("$",0,f) if f>0 else -1)}}{{set("l",inv.find("$",f+1))}}{{set("dl",inv[f:l] if f>=0 and l>=0 else inv[f::] if f>=0 and l==-1 else "")}}{{set("g",dl.split("|"))}}{{set("a",(g[0].replace("$","") if len(g)>1 and m!="p" else "") if dl!="" else x if m!="p" else "")}}{{set("d",int(g[1].replace(" (","").replace(")","")) if len(g)>1 else 0)}} -title "{{name if m!="h" else "How to Use"}}{{" adds "+str(n)+" " if m=="+" else " searches for a " if (m=="?" or (m=="-" and a.lower() not in inv.lower())) else " removes "+str(min(-n,d))+" " if m=="-" and dl!="" else ""}}{{a}}{{"" if n<2 and n>-2 else "s "}}{{"" if m=="h" else "'s" if m=="p" else " to their" if m=="+" else " from their" if (m=="-" and dl!="") else " in their"}} Inventory!" {{set("nl",("$"+a+"| ("+(str(n+d)+")")+"\n" if (n+d)>0 else ""))}}{{set_cvar("inv",(inv if inv[-1:]=="\n" else inv+"\n")+nl if dl=="" else inv.replace(dl,nl)) if m in "+-" and a!="" else ""}} -desc  "{{"__"+" "*200+"__\n"}}
{{(str(inv.replace("$","").replace("|","").replace("(1)","")) if inv!="" else "*Empty*") if m=="p" else (nl.replace("$","").replace("|","") if n+d>0 else "*None*") if m in "?+-" else ""}}" {{"" if m!="h" else get_gvar("8b40e3a0-528c-4747-a4c2-a0b5022af36a")}} {{"-footer \"!inv help for more info\"" if m!="h" else ""}} -color <color> -thumb https://goo.gl/6Zowo5 %1% %2% %3%
```