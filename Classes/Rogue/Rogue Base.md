## Stroke of Luck
```GN
!servalias luck embed
{{set("lvl", int(Rogue))}}
{{set("counter", "Stroke of Luck")}}
{{create_cc_nx(counter, 0, "1", "short", "bubble") if lvl>=20 else 0}}
{{mod_cc(counter, -1, True)}}
-title "<name> Has a Stroke of Luck!"
-desc "At 20th level, if your attack misses a target within range, you can turn the miss into a hit. Alternatively, if you fail an ability check, you can treat the d20 roll as a 20.

Once you use this feature, you can't use it again until you finish a short or long rest."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Rogue | PHB 97" -color <color> -thumb <image>
```