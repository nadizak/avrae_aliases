## Fighting Spirit
```GN
!servalias spirit embed
{{set("lvl", int(Fighter))}}
{{set("counter", "Fighting Spirit")}}
{{create_cc_nx(counter, 0, "3", "long", "bubble") if lvl>=3 else 0}}
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