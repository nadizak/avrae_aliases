## Channel Divinity
```GN
!servalias channel embed
{{useCleric=int(Paladin)<=int(Cleric)}}
{{lvl=int(Cleric) if useCleric else int(Paladin)}}
{{counter="Channel Divinity"}}
{{create_cc_nx(counter, 0, "6", "short") if lvl else 0}}
{{totalUses=1 if (not useCleric or lvl<6) else 2 if lvl<18 else 3}}
{{mod_cc(counter, -6/totalUses, True) if lvl else 0}}
{{set("current", int(get_cc(counter)*totalUses/6))}}
-title "<name> Uses {{counter}}."
-desc "Your oath allows you to channel divine energy to fuel magical effects. Each Channel Divinity option provided by your oath explains how to use it. When you use your Channel Divinity, you choose which option to use. You must then finish a short or long rest to use your Channel Divinity again. Some Channel Divinity effects require saving throws. When you use such an effect from this class, the DC equals your spell save DC ofr that class."
{{f'-f "Cleric DC|{8+proficiencyBonus+wisdomMod}"' if int(Cleric) else ''}}
{{f'-f "Paladin DC|{8+proficiencyBonus+charismaMod}"' if int(Paladin) else ''}}
-f "{{counter}}|{{'◉'*current + '〇'*(totalUses-current)}}"
-footer "{{"Cleric | 58-59" if useCleric else "Paladin | 85"}}" -color <color> -thumb <image>
```