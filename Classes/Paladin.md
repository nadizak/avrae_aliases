## All in One Paladin Alias
**Credit to @silverbass#2407**
```python
!servalias paladin embed 
{{k,r,w,l,a,b="\n###\n","&*&",get_gvar("71c8e803-890a-4944-afb7-c658d6a91aeb").split("\n"),int(PaladinLevel) if exists("PaladinLevel") else level,"&1&".lower(),"&2&".lower()}}{{f,u,g=w[4],w[5],[z.split("|") for z in get_gvar(w[1]).split(k)]}}{{c=[z[0] for z in g if a in z[0].lower()]}}{{c=g[3][0] if a in "cd" else c[0] if c else ""}}{{q=[z.split("|") for z in get_gvar(w[2]).split(k)]}}{{m=[z[0] for z in q if b in z[0].lower()]}}{{m=m[0] if m else ""}}{{x,y=[z[0] for z in g].index(c) if c in [z[0] for z in g] else 0,[z[0] for z in q].index(m) if m in [z[0] for z in q] else 0}}{{h=min(get_cc(c),int(b) if b.isdigit() else 5 if b in g[x][4] else 0) if x==1 and cc_exists(c) else min(9,max(1,int(b if b.isdigit() else 1))) if x==2 else 1}}{{v=get_slots(h)>0 if x==2 else (cc_exists(c) and get_cc(c)>0 and (m if x==3 else 1))}}
-title "{{name+(" uses " if v else " tries to use ")+("a CRITICAL " if x==2 and "crit" in r else "a ")+g[x][0]+(": "+g[x][3] if x==1 and b in g[x][4] else ": "+str(h) if x==1 else (w[6] if f in r else w[7] if u in r else "") if x==2 else "")+"!" if c else "Paladin"}}"
-desc "{{get_gvar(w[0]) if not c or (x==3 and not m) else g[x][1]+("\n**DC:** "+str(charismaMod+8+proficiencyBonus) if x==3 else "") if v else g[x][2] if cc_exists(c) or x==2 else w[3]}}"
{{"-f \""+m+"|"+q[y][1]+"\"" if v and x==3 and m else ""}}
{{"-f 'Healing|"+(str(h) if x==1 else str(vroll("1d6+"+str(max(1,charismaMod)))) if y==5 else "")+"'" if v and ((x==1 and b.isdigit()) or y==5) else ""}}
{{"-f 'Damage|"+str(vroll(str((min(h,4)+(2 if f in r or u in r else 1))*(2 if "crit" in r else 1))+"d8"))+"'" if v and x==2 else ""}}
{{(mod_cc(c,-h) if x!=2 else use_slot(h)) if v else ""}}{{"-f 'Spell Slots|"+slots_str(h)+"'" if x==2 else "-f '"+c+"|"+(cc_str(c) if cc_exists(c) else "*None*")+"'" if c else ""}}
-color <color> -thumb <image>
```

## Divine Sense
```python
!servalias divinesense embed
{{set("lvl", int(PaladinLevel))}}
{{set("counter", "Divine Sense")}}
{{mod_cc(counter, -1, True) if lvl else 0}}
-title "<name> Focuses Their Divine Sense."
-desc "The presence of strong evil registers on your senses like a noxious odor, and powerful good rings like heavenly music in your ears. As an action, you can open your awareness to detect such forces. Until the end of your next turn, you know the location of any celestial, fiend, or undead within 60 feet of you that is not behind total cover. You know the type (celestial, fiend, or undead) of any being whose presence you sense, but not its identity (the vampire Count Strahd von Zarovich, for instance). Within the same radius, you also detect the presence of any place or object that has been consecrated or desecrated, as with the hallow spell.
You can use this feature {{1+charismaMod}} times. When you finish a long rest, you regain all expended uses."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Paladin | PHB 84" -color <color> -thumb <image>
```

## Lay on Hands
```python
!servalias layonhands embed
{{set("lvl", int(PaladinLevel))}}
{{args="%1%%2%%"}}{{args=args[:args.index("%")]}}
{{selfHeal="self" in args or "me" in args}}
{{args=''.join([i for i in args if i.isdigit()])}}
{{spent=int(args) if args.isdigit() else 1}}
{{set("counter", "Lay on Hands")}}
{{mod_cc(counter, -1*spent, True) if lvl else 0}}
{{set_hp(min(hp, get_hp()+spent)) if selfHeal else 0}}
-title "<name> Draws Healing Power from the Divine."
-desc "You have a pool of healing power that replenishes when you take a long rest. With that pool, you can restore a total number of hit points equal to your paladin level x 5. As an action, you can touch a creature and draw power from the pool to restore a number of hit points to that creature, up to the maximum amount remaining in your pool.

Alternatively, you can expend 5 hit points from your pool of healing to cure the target of one disease or neutralize one poison affecting it. You can cure multiple diseases and neutralize multiple poisons with a single use of Lay on Hands, expending hit points separately for each one.

This feature has no effect on undead and constructs."
-f "{{counter}}|{{get_cc(counter)}} / {{get_cc_max(counter)}}"
-f "Healing Given|{{spent}}"
{{('-f "Current HP|' + str(get_hp()) + ' / ' + str(hp) + '"') if selfHeal else ''}}
-footer "Paladin | PHB 84" -color <color> -thumb <image>
```

## Divine Smite
```python
!servalias smite embed
{{args = "%1%%2%%"}}{{args=args[:args.index("%")]}}
{{crit = "crit" in args}}
{{args=''.join([i for i in args if i.isdigit()])}}
{{damageType = "d8 [radiant]"}}
{{spellLevel = int(args) if args.isdigit() else 1}}
{{use_slot(spellLevel)}}
{{damage = vroll(str(min(spellLevel+1, 5) * (2 if crit else 1)) + damageType)}}
{{fiendDamage = vroll(str(2 if crit else 1) + damageType)}}
-title "<name> uses Divine Smite!" 
-desc "When you hit a creature with a melee weapon attack, you can expend one spell slot to deal radiant damage to the target, in addition to the weapon’s damage. The damage increases by 1d8 if the target is an undead or a fiend." 
-f "Level {{spellLevel}} Slots | {{'◉'*get_slots(spellLevel) + '〇'*(get_slots_max(spellLevel)-get_slots(spellLevel))}}" 
-f "Damage {{"(***CRIT!***)" if crit else ""}}| {{str(damage)}}" 
-f "Fiend / Undead Additional Damage {{"(***CRIT!***)" if crit else ""}}| {{str(fiendDamage)}} " 
-footer "Paladin | PHB 85" 
-color <color>
```

## Channel Divinity
**See the Cleric Base aliases**

## Aura of Protection
```python
!servalias pldaura embed
{{lvl=int(PaladinLevel)}}
-title "<name> Emits an Aura of Protection"
-desc "You and allies within 10 feet of you receive the following benefits while you are conscious:
{{f"\t **\*** A +{charismaMod} to saving throws. \< **!snippet {name.lower()} -b \"+{charismaMod}[{name}]\"** \>" if lvl>=6 else ''}}
{{'\t **\*** Immunity to the frightened condition' if lvl>=10 else ''}}"
```
