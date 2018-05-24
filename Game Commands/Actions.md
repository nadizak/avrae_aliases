## Grapple
```GN
!servalias grapple c athletics 
-title "[charname] makes an Athletics check! (Grapple)" 
-phrase "The target must make an opposed Strength (Athletics) or Dexterity (Acrobatics) check. If you succeed, it is subjected to the grappled condition."
```

## Overrun
```GN
!servalias overrun c athletics
-title "<name> makes an Athletics check! (Overrun)"
-phrase "The target must make an opposed Strength (Athletics) check. If you succeed, you can move through the hostile creature's space once this turn."
```

## Potion
```GN
!servalias potion embed
{{set("name", "%1%.lower())}}
{{set("potion", "Supreme " if name == "supreme" else "Superior " if name == "superior" else "Greater " if name == "greater" else "")}}
{{set("rol", "10d4+20" if name == "supreme" else "8d4+8" if name == "superior" else "4d4+4" if name == "greater" else "2d4+2")}}
{{set("heal", vroll(rol))}}
{{set_hp(min(hp, heal.total + currentHp))}}
-title "<name> drinks a Potion of {{potion}}Healing!"
-desc "<name> drank a Potion of {{potion}}Healing and heals for {{rol}} hit points."
-f "Healing Done | {{str(heal)}}"
-f "Hit Points | {{get_hp()}}/{{hp}}"
```

## Prone
```GN
!servalias prone c athletics
-title "<name> makes an Athletics check! (Prone)"
-phrase "The target must make an opposed Strength (Athletics) or Dexterity (Acrobatics) check. If you succeed, the target is knocked prone."
```

## Push
```GN
!servalias push c athletics
-title "<name> makes an Athletics check! (Push)"
-phrase "The target must make an opposed Strength (Athletics) or Dexterity (Acrobatics) check. If you succeed, the target is pushed 5 feet away from you."
```

## Battering Ram
```GN
!servalias ram c str -title '<name> uses a Portable Ram!' -b '4 [Ram]' -phrase 'You can use a portable ram to break down doors. When doing so, you gain a +4 bonus on the Strength check. One other character can help you use the ram, giving you advantage on this check.'
```

## Scroll
```GN
!servalias scroll multiline
!embed {{set("level", int("%1%") if "%1"+"%"!="%1%" else 0)}} {{set("dc", str(10+level))}} {{set("mod", str(max(charismaMod, intelligenceMod, wisdomMod)))}} {{set("result", vroll("1d20+" + mod))}} {{set("success", (result.total>=int(dc)))}} {{'-t "<name> attempts to use a level %1% scroll"' if level else '-t "Spell Scrolls"'}} -desc "If the spell is of a higher level than you can normally cast, you must make an ability check using your spellcasting ability to determine whether you cast it successfully. The DC equals 10 + the spell's level." {{('-f "DC|' + dc + '"') if level else ''}} {{('-f "Ability Check|' + str(result) + '"') if level else ''}} {{('-f "Result|' + ("Success" if success else "Failure") + '"') if level else ''}}
!cast %2% %3% %4% %5% %6% %7% %8% %9% %0%
```

## Shove
```GN
!servalias shove c athletics
-title "<name> makes an Athletics check! (Shove)"
-phrase "The target must make an opposed Strength (Athletics) or Dexterity (Acrobatics) check. If you succeed, the target is knocked prone or pushed 5 feet away from you."
```

## Tumble
```GN
!servalias tumble c acrobatics
-title "<name> makes an Acrobatics check! (Tumble)"
-phrase "The target must make an opposed Dexterity (Acrobatics) check. If you succeed, you can move through the hostile creature's space once this turn."
```