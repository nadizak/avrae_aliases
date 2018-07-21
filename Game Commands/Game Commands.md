## Heal
```python
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
```python
!servalias hitdice embed
{{set('die', '' if "%1"+"%"=="%1%" else 'd%1%' if '%1%'[0] != 'd' else '%1%')}}
{{set('used', '%2%' if '%2'+'%'!='%2%' else '1')}}
{{set('dieStr', "Hit Dice (" + die + ")")}}
{{mod_cc(dieStr, -1*int(used), True) if die else 0}}
{{set("heal", vroll(used+die+"+"+str(constitutionMod*int(used))))}}
{{set_hp(min(hp, heal.total + currentHp)) if die else 0}}
{{counters=get_raw().consumables.custom}}
-title "{{(name + ' takes a Short Rest!') if die else 'Hit Dice'}}" 
-desc "{{get_gvar("8e7251ab-1596-48b0-976d-fdc1ecbbab94")}}"
{{('-f "Healing Received|' + str(heal) + '"') if die else ''}} 
{{('-f "Hit Points|' + str(get_hp()) + ' / ' + str(hp) + '"') if die else ''}} 
{{('-f "Hit Dice (d6)|' + str(get_cc("Hit Dice (d6)")) + ' / ' + str(get_cc_max("Hit Dice (d6)")) + '"') if "Hit Dice (d6)" in counters else ''}}
{{('-f "Hit Dice (d8)|' + str(get_cc("Hit Dice (d8)")) + ' / ' + str(get_cc_max("Hit Dice (d8)")) + '"') if "Hit Dice (d8)" in counters else ''}} 
{{('-f "Hit Dice (d10)|' + str(get_cc("Hit Dice (d10)")) + ' / ' + str(get_cc_max("Hit Dice (d10)")) + '"') if "Hit Dice (d10)" in counters else ''}} 
{{('-f "Hit Dice (d12)|' + str(get_cc("Hit Dice (d12)")) + ' / ' + str(get_cc_max("Hit Dice (d12)")) + '"') if "Hit Dice (d12)" in counters else ''}}
-footer "Adventuring | PHB 186" 
-color <color> -thumb <image>
```

## HP Roll (For level up hp)
```python
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

## Surprise Rounds
```python
!servalias surprise embed
-title "Surprise Rounds"
-desc "If you’re surprised, you can’t move or take an action on your first turn of the combat, and you can’t take a reaction until that turn ends. A member of a group can be surprised even if the other members aren’t."
-footer "PHB 189"
```

## Short Rest
```python
!servalias sr multiline
!embed {{ds=" (%2%)" if "%2%" in "d4d6d8d10d12d20" else ""}}{{ds=" (d"+"%1%".split("d")[1]+")" if "d" in "%1%" else ds}}{{cc="Hit Dice"+ds}}{{du=0 if "%1%" == "%1"+"%" or not cc_exists(cc) else int("%1%".split("d")[0]) if "d" in "%1%" else int("%1%")}}{{du=min(get_cc(cc),du) if cc_exists(cc) else 0}}{{mod_cc(cc, -du) if cc_exists(cc) else ""}}{{roll=(str(du)+str(hd if exists("hd") and ds=="" else ds[2:-1]))+"+"+str(du*constitutionMod)}}{{vheal=vroll("0" if du == 0 else roll)}}{{set_hp(min(hp, vheal.total + currentHp))}}{{wlvl=int(WarlockLevel) if exists("WarlockLevel") else 0}}{{splvl=min(ceil(int(wlvl)/2),5)}}{{numSlots=0 if wlvl==0 else 1 if wlvl<= 1 else 2 if wlvl< 11 else 3 if wlvl< 17 else 4}}{{set_slots(splvl, min(numSlots + get_slots(splvl), get_slots_max(splvl))) if wlvl>0 else ""}} -title "<name> takes a Short Rest." -desc "<name> spends {{du}}{{"" if ds=="" else " "+ds[2:-1]}} hit die and recovers {{vheal.total}} hit points. {{"They also recover "+str(numSlots)+" Level "+str(splvl)+" spell slots." if wlvl>0 else ""}}" -f "Healing Recieved|{{str(vheal)}}" -f "Current HP: | {{min(hp, (vheal.total+ currentHp))}}/{{hp}}{{set_hp(min(hp, (vheal.total + currentHp)))}}" {{"-f \""+cc+("" if ds else " ("+str(hd)+")")+" | "+cc_str(cc)+"\"" if cc_exists(cc) else ""}} -color <color> -footer "Adventuring | PHB 186" {{"-f \"Spell Slots| "+slots_str(splvl)+"\"" if wlvl>0 else ""}}
!g sr -h
```

## Money
**Credit to @silverbass#2407**
```python
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
```python
!servalias inv embed {{set("x","&2&" if "%2%"!="%2"+"%" else "")}}{{set("m","%1%")}}{{set("m","h" if m in "help" else "r" if m in "delete" else "p" if x=="" else m if m=="+" or m=="-" or m=="?" else "p")}}{{set("n",int("%3%") if "%3%".isdigit() else 1)}}{{set("n",int(m+str(n)) if m in "+-" else 0)}}{{set_cvar("inv","") if m=="r" or not exists("inv") else ""}}{{set("m","p" if m=="r" else m)}}{{set("f",inv.lower().find(x.lower()) if x!="" else -1)}}{{set("f",-1 if f<0 else 0 if f==0 else f if inv[f]=="$" else inv.rfind("$",0,f) if f>0 else -1)}}{{set("l",inv.find("$",f+1))}}{{set("dl",inv[f:l] if f>=0 and l>=0 else inv[f::] if f>=0 and l==-1 else "")}}{{set("g",dl.split("|"))}}{{set("a",(g[0].replace("$","") if len(g)>1 and m!="p" else "") if dl!="" else x if m!="p" else "")}}{{set("d",int(g[1].replace(" (","").replace(")","")) if len(g)>1 else 0)}} -title "{{name if m!="h" else "How to Use"}}{{" adds "+str(n)+" " if m=="+" else " searches for a " if (m=="?" or (m=="-" and a.lower() not in inv.lower())) else " removes "+str(min(-n,d))+" " if m=="-" and dl!="" else ""}}{{a}}{{"" if n<2 and n>-2 else "s "}}{{"" if m=="h" else "'s" if m=="p" else " to their" if m=="+" else " from their" if (m=="-" and dl!="") else " in their"}} Inventory!" {{set("nl",("$"+a+"| ("+(str(n+d)+")")+"\n" if (n+d)>0 else ""))}}{{set_cvar("inv",(inv if inv[-1:]=="\n" else inv+"\n")+nl if dl=="" else inv.replace(dl,nl)) if m in "+-" and a!="" else ""}} -desc  "{{"__"+" "*200+"__\n"}}
{{(str(inv.replace("$","").replace("|","").replace("(1)","")) if inv!="" else "*Empty*") if m=="p" else (nl.replace("$","").replace("|","") if n+d>0 else "*None*") if m in "?+-" else ""}}" {{"" if m!="h" else get_gvar("8b40e3a0-528c-4747-a4c2-a0b5022af36a")}} {{"-footer \"!inv help for more info\"" if m!="h" else ""}} -color <color> -thumb https://goo.gl/6Zowo5 %1% %2% %3%
```