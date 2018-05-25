## Action Surge
```GN
!servalias action embed
{{set("lvl", int(Fighter))}}
{{set("counter", "Action Surge")}}
{{create_cc_nx(counter, 0, "2", "short", "bubble") if lvl else 0}}
{{mod_cc(counter, -2 if lvl<17 else 1, True) if lvl else 0}}
{{set("total", 1 if lvl<17 else 2)}}
{{set("current", 0 if lvl<17 else get_cc(counter))}}
-title "<name> Goes Beyond Their Limits!"
-desc "You can push yourself beyond your normal limits for a moment. On your turn, you can take one additional action on top of your regular action and a possible bonus action.
Once you use this feature, you must finish a short or long rest before you can use it again. Starting at 17th level, you can use it twice before a rest, but only once on the same turn."
-f "{{counter}}|{{'◉'*current + '〇'*(total-current)}}"
-footer "Fighter | PHB 70" -color <color> -thumb <image>
```

## Second Wind
```GN
!servalias secondwind embed
{{set("lvl", int(Fighter))}}
{{set("counter", "Second Wind")}}
{{create_cc_nx(counter, 0, "1", "short", "bubble") if lvl else 0}}
{{mod_cc(counter, -1, True) if lvl else 0}}
{{set("healed", vroll("1d10+" + str(level-int(Fighter)))) if lvl else 0}}
{{set_hp(min(hp, get_hp()+healed.total))}}
-title "<name> Takes a Breath and Regains Stamina!"
-desc "You have a limited well of stamina that you can draw on to protect yourself from harm. On your turn, you can use a bonus action to regain hit points equal to 1d10 + your fighter level.
Once you use this feature, you must finish a short or long rest before you can use it again."
-f "Regained|{{str(healed)}}"
-f "Current HP|{{get_hp()}}/{{hp}}"
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Fighter | PHB 70" -color <color> -thumb <image>
```