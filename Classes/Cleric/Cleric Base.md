## Channel Divinity
```python
!servalias channel embed
{{useCleric=exists("ClericLevel")}}
{{lvl=int(ClericLevel) if useCleric else int(PaladinLevel)}}
{{counter="Channel Divinity"}}
{{mod_cc(counter, -1, True) if lvl else 0}}
-title "<name> Uses {{counter}}."
-desc "Your oath allows you to channel divine energy to fuel magical effects. Each Channel Divinity option provided by your oath explains how to use it. When you use your Channel Divinity, you choose which option to use. You must then finish a short or long rest to use your Channel Divinity again. Some Channel Divinity effects require saving throws. When you use such an effect from this class, the DC equals your spell save DC ofr that class."
-f "DC|{{get_raw().spellbook.dc}}"
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "{{"Cleric | 58-59" if useCleric else "Paladin | 85"}}" -color <color> -thumb <image>
```