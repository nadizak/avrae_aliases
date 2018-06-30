## Booming Blade
```GN
!servalias boom embed
{{set("dice", 1 if level < 5 else 2 if level < 11 else 3 if level < 17 else 4)}}
{{set("dmg", vroll(str(dice) + "d8 [thunder]"))}}
{{"" if level < 5 else "-d \"" + str(dice - 1) + "d8 [thunder, boom]\""}}
-f "Booming Blade | On a hit, if the target willingly moves before then, it immediately takes {{str(dmg)}} thunder damage." 
```

## Green-Flame Blade
```GN
!servalias gfb embed
{{set("mod", str(max(charismaMod, intelligenceMod)))}}
{{set("dice", " " if level < 5 else "1d8" if level < 11 else "2d8" if level < 17 else "3d8")}}
{{set("dmg", vroll(dice + (" + " if level >= 5 else "") + mod + " [fire]"))}}
{{"" if level < 5 else "-d \"" + dice + " [fire, gfb]\""}}
-f "Green-Flame Blade | On a hit, a different creature of your choice you can see within 5 feet of your target takes {{str(dmg)}} damage." 
```

## Toll the Dead
```GN
!servalias toll embed
{{set("mod", max(charismaMod, wisdomMod, intelligenceMod))}}
{{set("y", 4 if level > 16 else 3 if level > 10 else 2 if level > 4 else 1)}}
{{set("z", vroll(str(y)+"d8"))}}
{{set("Z", vroll(str(y)+"d12"))}}
-title "<name> casts Toll the Dead!"
-desc "<name> points at one creature they can see within range (60ft), and the sound of a dolorous bell fills the air around it for a moment. The target must succeed on a DC{{mod+8+proficiencyBonus}} Wisdom saving throw or take {{y}}d8 necrotic damage. If the target is missing any of its hit points, it instead takes {{y}}d12 necrotic damage."
-f "Undamaged | {{z}} if they fail"
-f "Damaged | {{Z}} if they fail"
-color <color> -thumb <image>
```
