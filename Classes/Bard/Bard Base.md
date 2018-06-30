## Bardic Inspiration
```GN
!servalias inspire embed
{{lvl=int(Bard)}}
{{counter="Bardic Inspiration"}}
{{die="d12" if lvl>=15 else "d10" if lvl>=10 else "d8" if lvl>=5 else "d6"}}
{{target="%1%" if "%1"+"%"!="%1%" else ""}}
{{total="charismaMod" if charismaMod>=1 else "1"}}
{{create_cc_nx(counter, 0, total, "long" if lvl<5 else "short", "bubble") if lvl else 0}}
{{mod_cc(counter, -1, True)}}
-title "<name> Grants Inspiration{{f" To {target}" if target else ""}}!"
-desc "You can use a bonus action on your turn to choose one creature other than yourself within 60 feet of you who can hear you. That creature gains one Bardic Inspiration die, a {{die}}.

Once within the next 10 minutes, the creature can roll the die and add the number rolled to one ability check, attack roll, or saving throw it makes. The creature can wait until after it rolls the d20 before deciding to use the Bardic Inspiration die, but must decide before the DM says whether the roll succeeds or fails. Once the Bardic Inspiration die is rolled, it is lost. A creature can have only one Bardic Inspiration die at a time.

You can use this feature {{get_cc_max(counter)}} times. You regain any expended uses when you finish a long rest. Your Bardic Inspiration die changes when you reach certain levels in this class. The die becomes a d8 at 5th level, a d10 at 10th level, and a d12 at 15th level."
-f "Inspiration Die|{{die}}"
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Bard | PHB 53-54"
-color <color> -thumb <image>
```

## Jack of All Trades
```GN
!servsnippet jack -b "{{int(proficiencyBonus/2)}}[Jack of All Trades]"
```

## Song of Rest
```GN
!servalias songofrest embed
{{lvl=int(Bard)}}
{{die="d12" if lvl>=17 else "d10" if lvl>=13 else "d8" if lvl>=9 else "d6"}}
{{mod_cc("n/a", -1, True) if not lvl else 0}}
-title "<name> Performs a Song of Rest."
-desc "If you or any friendly creatures who can hear you make a performance regain hit points by spending hit dice at the end of the short rest, each of those creatures regains an extra 1{{die}} hit points."
-f "Additional Die|1{{die}}"
-footer "Bard | PHB 54"
-color <color> -thumb <image>
```