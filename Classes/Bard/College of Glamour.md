## Bardic Inspiration
```GN
!servalias glaminspire embed
{{lvl=int(Bard)}}
{{counter="Bardic Inspiration"}}
{{die="14" if lvl>=15 else "11" if lvl>=10 else "8" if lvl>=5 else "5"}}
{{target="&*&" if "&*"+"&"!="&*&" else ""}}
{{total="charismaMod" if charismaMod>=1 else "1"}}
{{create_cc_nx(counter, 0, total, "long" if lvl<5 else "short", "bubble") if lvl else 0}}
{{mod_cc(counter, -1, True)}}
-title "<name> Grants Inspiration{{f" To {target}" if target else ""}}!"
-desc "When you join the College of Glamour at 3rd level, you gain the ability to weave a song of fey magic that imbues your allies with vigor and speed.

As a bonus action, you can expend one use of your Bardic Inspiration to grant yourself a wondrous appearance. When you do so, choose a number of creatures you can see and that can see you within 60 feet of you, up to a number equal to your Charisma modifier (minimum of one). Each of them gains 5 temporary hit points. When a creature gains these temporary hit points, it can immediately use its reaction to move up to its speed, without provoking opportunity attacks.

The number of temporary hit points increases when you reach certain levels in this class, increasing to 8 at 5th level, 11 at 10th level, and 14 at 15th level."
-f "Temp HP Gained|{{die}}"
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "College of Glamour | XGTE 14"
-color <color> -thumb <image>
```