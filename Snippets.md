## Bless
```GN
!servsnippet bless -b 1d4[Bless]
```
## Booming Blade
**Credit to Toothless#7854**
```GN
!servsnippet boom
{{set("dice", 1 if level < 5 else 2 if level < 11 else 3 if level < 17 else 4)}}
{{set("dmg", vroll(str(dice) + "d8 [thunder]"))}}
{{"" if level < 5 else "-d \"" + str(dice - 1) + "d8 [thunder, boom]\""}}
-f "Booming Blade | On a hit, if the target willingly moves before then, it immediately takes {{str(dmg)}} thunder damage."
```

## Bracers of Archery
```GN
!servsnippet bracers -d "2[Bracers of Archery]"
```

## Additional d6
```GN
!snippet d6 -f "d6 Damage|{{vroll("1d6")}}"
```

## Additional d8
```GN
!snippet d8 -f "d8 Damage|{{vroll("1d8")}}"
```

## Additional d10
```GN
!snippet d10 -f "d10 Damage|{{vroll("1d10")}}"
```

## Green Flame Blade
**Credit to Toothless#7854**
```GN
!servsnippet gfb
{{set("mod", str(max(charismaMod, intelligenceMod)))}}
{{set("dice", " " if level < 5 else "1d8" if level < 11 else "2d8" if level < 17 else "3d8")}}
{{set("dmg", vroll(dice + (" + " if level >= 5 else "") + mod + " [fire]"))}}
{{"" if level < 5 else "-d \"" + dice + " [fire, gfb]\""}}
-f "Green-Flame Blade | On a hit, a different creature of your choice you can see within 5 feet of your target takes {{str(dmg)}} damage."
```

## Guidance
```GN
!servsnippet guidance -b "1d4 [Guidance]"
```

## Greater Weapon Master
```GN
!servsnippet gwm -b "-5" -d "10 [gwm]"
```

## Hex
```GN
!servsnippet hex -d "1d6[Necrotic]"
```

## Hunter's Mark
```GN
!servsnippet mark -d "1d6 [Mark]"
```

## Pass Without Trace
```GN
!servsnippet pwt -b "10[Pass Without Trace]"
```

## Rage
```GN
!servsnippet rage -d "{{2 if int(Barbarian)<8 else (3 if int(Barbarian)<15 else 4)}} [Rage]"
```

## Resist
```GN
!servsnippet resist -b "1d4 [Resistance]"
```

## Sharpshooter Feat
```GN
!servsnippet sharp -b "-5" -d "10 [Sharpshooter]"
```

## Sneak Attack
```GN
!servsnippet sneak -d1 "{{ceil(int(Rogue)/2)}}d6 [Sneak Attack]"
```
