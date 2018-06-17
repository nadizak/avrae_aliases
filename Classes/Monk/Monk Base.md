## Ki Points
```GN
!servalias ki embed
{{lvl=int(Monk)}}
{{counter="Ki Points"}}
{{mod=int("%1%") if "%1"+"%"!="%1%" else 0}}
{{nosign="+" not in "&*&" and "-" not in "&*&"}}
{{create_cc_nx(counter, 0, "Monk", "short", "bubble") if lvl>=2 else 0}}
{{mod_cc(counter, mod * (-1 if nosign else 1), True) if "+" not in "&*&" else 0}}
{{mod_cc(counter, mod) if "+" in "&*&" else 0}}
-title "<name> Expends Their Ki!"
-desc "Starting at 2nd level, your access to the mystic energy Ki is represented by a number of ki points. Your monk level determines the number of points you have, as shown in the Ki Points column of the Monk table.

You can spend these points to fuel various ki features. You start knowing three such features: Flurry of Blows, Patient Defense, and Step of the Wind, You learn more ki features as you gain levels in this class,

When you spend a ki point. it is unavailable until you finish a short or long rest, at the end of which you draw all of your expended ki back into yourself. You must spend at least 30 minutes of the rest meditating to regain your ki points."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Monk | PHB 78" -color <color> -thumb <image>
```

## Flurry of Blows
```GN
!servalias flurry embed
{{lvl=int(Monk)}}
{{counter="Ki Points"}}
{{create_cc_nx(counter, 0, "Monk", "short", "bubble") if lvl>=2 else 0}}
{{mod_cc(counter, -1)}}
-title "<name> Unleashes a Flurry of Blows!"
-desc "Immediately after you take the Attack action on your turn, you can spend 1 ki point to make two unarmed strikes as a bonus action."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Monk | PHB 78" -color <color> -thumb <image>
```

## Patient Defense
```GN
!servalias patient embed
{{lvl=int(Monk)}}
{{counter="Ki Points"}}
{{create_cc_nx(counter, 0, "Monk", "short", "bubble") if lvl>=2 else 0}}
{{mod_cc(counter, -1)}}
-title "<name> Enters a Defensive Stance!"
-desc "You can spend 1 ki point to take the Dodge action as a bonus action on your turn."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Monk | PHB 78" -color <color> -thumb <image>
```

## Step of the Wind
```GN
!servalias windstep embed
{{lvl=int(Monk)}}
{{counter="Ki Points"}}
{{create_cc_nx(counter, 0, "Monk", "short", "bubble") if lvl>=2 else 0}}
{{mod_cc(counter, -1)}}
-title "<name> Moves With Ludicrous Speed!"
-desc "You can spend 1 ki point to take the Disengage or Dash action as a bonus action on your turn, and your jump distance is doubled for the turn."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Monk | PHB 78" -color <color> -thumb <image>
```

## Deflect Missiles
```GN
!servalias deflect embed
{{lvl=int(Monk)}}
{{counter="Ki Points"}}
{{catch=("%1"+"%" != "%1%")}}
{{create_cc_nx(counter, 0, "Monk", "short", "bubble") if lvl>=2 else 0}}
{{mod_cc(counter, -1) if catch else 0}}
{{reduce=vroll(f"1d10+{dexterityMod}+{Monk}")}}
-title "<name> {{"Deflects" if not catch else "Catches"}} the Projectile!"
-desc "Starting at 3rd level, you can use your reaction to deflect or catch the missile when you are hit by a ranged weapon attack. When you do so, the damage you take from the attack is reduced by 1d10 + your Dexterity modifier + your monk level.

If you reduce the damage to 0, you can catch the missile if it is small enough for you to hold in one hand and you have at least one hand free. If you catch a missile in this way, you can spend 1 ki point to make a ranged attack (20/60 feet) with the weapon or piece of ammunition you just caught, as part of the same reaction. You make this attack with proficiency, regardless of your weapon proficiencies, and the missile counts as a monk weapon for the attack."
{{f'-f "Damage Reduction|{reduce}"' if not catch else ''}}
{{f'-f "{counter}|{"◉"*get_cc(counter)}{"〇"*(get_cc_max(counter)-get_cc(counter))}"' if catch else ''}}
-footer "Monk | PHB 78" -color <color> -thumb <image>
```

## Empty Body
```GN
!servalias empty embed
{{lvl=int(Monk)}}
{{counter="Ki Points"}}
{{create_cc_nx(counter, 0, "Monk", "short", "bubble") if lvl>=18 else 0}}
{{mod_cc(counter, -4)}}
-title "<name> Focuses and Vanishes from Sight!"
-desc "Beginning at 18th level, you can use your action to spend 4 ki points to become invisible for 1 minute. During that time, you also have resistance to all damage but force damage.

Additionally, you can spend 8 ki points to cast the Astral Projection spell, without needing material components. When you do so, you can't take any other creatures with you."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Monk | PHB 79" -color <color> -thumb <image>
```