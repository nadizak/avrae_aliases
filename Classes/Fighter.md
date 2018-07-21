## All in One Fighter Alias
**Credit to @silverbass#2407**
```python
!servalias fighter embed 
{{p,w,l,a,b=proficiencyBonus,get_gvar("990dc1ad-ae0f-46b3-8126-8b562725c421").split("\n"),int(FighterLevel) if exists("FighterLevel") else level,"&1&".lower(),"&2&".lower()}}{{g,d=[z.split("|") for z in get_gvar(w[1]).split("\n###\n")],d if exists("d") else "d8" if l<10 else "d10" if l<18 else "d12"}}{{c=[z[0] for z in g if a in z[0].lower()]}}{{c=g[0][0] if a in "2nd" else g[3][0] if a=="bm" else c[0] if c else ""}}{{q=[z.split("|") for z in get_gvar(w[3 if "Arc" in c else 2]).split("\n###\n")]}}{{m=[z[0] for z in q if b in z[0].lower()]}}{{m=m[0] if m else ""}}{{x,y=[z[0] for z in g].index(c) if c in [z[0] for z in g] else 0,[z[0] for z in q].index(m) if m in [z[0] for z in q] else 0}}{{c=g[3][3] if x==3 else c}}{{v=cc_exists(c) and get_cc(c)>0 and (m if 5>x>2 else 1)}}
-title "{{name+(" uses " if v else " tries to use ")+g[x][0]+"!" if c else "Fighter"}}"
-desc "{{get_gvar(w[0]) if not c or (5>x>2 and not m) else g[x][1]+("\n**DC:** "+str(max(dexterityMod,strengthMod)+8+p) if x==3 else "\n**DC:** "+str(intelligenceMod+8+p) if x==4 else "") if v else g[x][2] if cc_exists(c) else w[4]}}"
{{h=vroll("1d10+"+str(l))}}{{"-f \"Healing|"+str(h)+"\" -f \"Hit Points|"+("" if set_hp(min(hp,h.total+get_hp())) else "")+str(get_hp())+" / "+str(hp)+"\"" if v and x==0 else ""}}
{{"-f \"AC Increase|"+str(vroll("1d8"))+"\"" if x==6 else ""}}
{{set_temphp(5) if x==7 and v else ""}}
{{"-f \""+m+"|"+q[y][1].replace("%D%",(str(vroll(q[y][(2 if l<18 else 3)])) if x==4 else ""))+"\"" if v and 5>x>2 and m else ""}}
{{("-f \"Bonus to Hit|"+str(vroll(d))+"\"" if "Pr" in m else "-f \"New AC|"+str(vroll(d+"+"+str(armor)))+"\"" if "Ev" in m else "-f \"Reduced By|"+str(vroll(d+"+"+str(dexterityMod)))+"\"" if "Pa" in m else "-f \"Damage|"+str(vroll(d))+"\"") if v and x==3 and m else ""}}
{{mod_cc(c,-1) if v else ""}}{{"-f \""+c+"|"+(cc_str(c) if cc_exists(c) else "*None*")+"\"" if c else ""}}
-color <color> -thumb <image>
```

## Action Surge
```python
!servalias action embed
{{set("lvl", int(FighterLevel))}}
{{set("counter", "Action Surge")}}
{{mod_cc(counter, -2 if lvl<17 else -1, True)}}
{{set("total", 1 if lvl<17 else 2)}}
{{set("current", 0 if lvl<17 else get_cc(counter))}}
-title "<name> Goes Beyond Their Limits!"
-desc "You can push yourself beyond your normal limits for a moment. On your turn, you can take one additional action on top of your regular action and a possible bonus action.
Once you use this feature, you must finish a short or long rest before you can use it again. Starting at 17th level, you can use it twice before a rest, but only once on the same turn."
-f "{{counter}}|{{'◉'*current + '〇'*(total-current)}}"
-footer "Fighter | PHB 70" -color <color> -thumb <image>
```

## Second Wind
```python
!servalias secondwind embed
{{set("lvl", int(FighterLevel))}}
{{set("counter", "Second Wind")}}
{{mod_cc(counter, -1, True)}}
{{set("healed", vroll("1d10+" + FighterLevel)) if lvl else 0}}
{{set_hp(min(hp, get_hp()+healed.total))}}
-title "<name> Takes a Breath and Regains Stamina!"
-desc "You have a limited well of stamina that you can draw on to protect yourself from harm. On your turn, you can use a bonus action to regain hit points equal to 1d10 + your fighter level.
Once you use this feature, you must finish a short or long rest before you can use it again."
-f "Regained|{{str(healed)}}"
-f "Current HP|{{get_hp()}}/{{hp}}"
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Fighter | PHB 72" -color <color> -thumb <image>
```

## Indomitable
```python
!servalias indom embed
{{lvl=int(FighterLevel)}}
{{counter="Indomitable"}}
{{mod_cc(counter, -1, True)}}
-title "<name> is Indomitable!"
-desc "Beginning at 9th level, you can reroll a saving throw that you fail. If you do so, you must use the new roll, and you can't use this feature again until you finish a long rest. You can use this feature twice between long rests starting at 13th level and three times between long rests starting at 17th level."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Fighter | PHB 72" -color <color> -thumb <image>
```

## Fighting Spirit
```GN
!servalias spirit embed
{{set("lvl", int(Fighter))}}
{{set("counter", "Fighting Spirit")}}
{{mod_cc(counter, -1, True) if lvl>=3 else 0}}
{{set("temphp", 5 if lvl<10 else 10 if lvl<15 else 15)}}
{{set_temphp(max(get_temphp(), temphp))}}
-title "<name> Focuses Intently on the Battle!"
-desc "Starting at 3rd level, your intensity in battle can shield you and help you strike true. As a bonus action on your turn, you can give yourself advantage on weapon attack rolls until the end of the current turn. When you do so, you also gain 5 temporary hit points. The number of temporary hit points increases when you reach certain levels in this class, increasing to 10 at 10th level and 15 at 15th level.
You can use this feature three times, and you regain all expended uses of it when you finish a long rest."
-f "Current HP|{{get_hp()}}/{{hp}} ({{get_temphp()}} temp)"
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Samurai | XGTE 31" -color <color> -thumb <image>
```