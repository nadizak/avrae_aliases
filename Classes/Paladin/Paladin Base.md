## Divine Sense
```GN
!servalias divinesense embed
{{set("lvl", int(Paladin))}}
{{set("counter", "Divine Sense")}}
{{create_cc_nx(counter, 0, "1+charismaMod", "long", "bubble") if lvl else 0}}
{{mod_cc(counter, -1, True) if lvl else 0}}
-title "<name> Focuses Their Divine Sense."
-desc "The presence of strong evil registers on your senses like a noxious odor, and powerful good rings like heavenly music in your ears. As an action, you can open your awareness to detect such forces. Until the end of your next turn, you know the location of any celestial, fiend, or undead within 60 feet of you that is not behind total cover. You know the type (celestial, fiend, or undead) of any being whose presence you sense, but not its identity (the vampire Count Strahd von Zarovich, for instance). Within the same radius, you also detect the presence of any place or object that has been consecrated or desecrated, as with the hallow spell.
You can use this feature {{1+charismaMod}} times. When you finish a long rest, you regain all expended uses."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Paladin | PHB 84" -color <color> -thumb <image>
```

## Lay on Hands
```GN
!servalias layonhands embed
{{set("lvl", int(Paladin))}}
{{args="%1%%2%%"}}{{args=args[:args.index("%")]}}
{{selfHeal="self" in args or "me" in args}}
{{args=''.join([i for i in args if i.isdigit()])}}
{{spent=int(args) if args.isdigit() else 1}}
{{set("counter", "Lay on Hands")}}
{{create_cc_nx(counter, 0, "Paladin*5", "long") if lvl else 0}}
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
```GN
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
```GN
!servalias pld_aura embed
{{lvl=int(Paladin)}}
-title "<name> Emits an Aura of Protection"
-desc "You and allies within 10 feet of you receive the following benefits while you are conscious:
{{f"\t **\*** A +{charismaMod} to saving throws. \< **!snippet {name.lower()} -b \"+{charismaMod}[{name}]\"** \>" if lvl>=6 else ''}}
{{'\t **\*** Immunity to the frightened condition' if lvl>=10 else ''}}"
```
