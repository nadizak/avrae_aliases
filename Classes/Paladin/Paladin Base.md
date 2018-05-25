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
-footer "Paladin | PHB 82" -color <color> -thumb <image>
```