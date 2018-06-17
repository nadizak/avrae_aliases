## Bigby's Hand
```GN
!alias bigby embed 
{{set("slevel", max(int(%1%),5))}}
{{set("adv",  "adv" == "%2%")}}
{{set("dis", "dis" == "%2%")}}
{{set("ifcrit", "crit" == "%2%")}}
{{set("roll", "2d20kh1" if adv else "2d20kl1" if dis else "1d20")}}
{{set("tohit", vroll(f"{roll}+{get_raw()['spellbook']['attackBonus']}"))}}
{{set("crit", ifcrit if ifcrit else tohit.total == (20+get_raw()['spellbook']['attackBonus']))}}
{{set("damageTotal", str((slevel -3) * 2 * (2 if crit else 1))+"d8 [Force]")}}
{{damage = vroll(damageTotal)}}
-title "<name> uses Bigby's Hand!"
-desc "<name> used a {{slevel}}th level spell slot and deals 4d8 + 2d8 per spell slot above fifth level on a hit."
-f "To Hit|{{"(***CRIT!***)" if crit else ""}}{{tohit}}"
-f "Damage | {{"(***CRIT!***)" if crit else ""}} {{damage}}"
```