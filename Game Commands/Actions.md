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
-color <color> -thumb <image>
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
!servalias scroll !multiline
{{args="%1%%2%%"}}{{args=args[:args.index("%")]}}
{{wizCopy="copy" in args or "book" in args or "wiz" in args}}
{{args=''.join([i for i in args if i.isdigit()])}}
{{spellLvl=int(args) if args.isdigit() else 5}}
{{dc=spellLvl+10}}
{{stats=[charismaMod, intelligenceMod, wisdomMod]}}
{{check="arc" if wizCopy else ["char", "int", "wis"][stats.index(max(stats))]}}
{{title=f"Copy a level {spellLvl} Spell." if wizCopy else f"Cast a level {spellLvl} Spell!"}}
!check {{check}} -title "<name> Attempts to {{title}}" -dc {{dc}} &*&
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

## Jump
```GN
!servalias jump embed
{{long='l' in "&*&"}}
{{high='h' in "&*&"}}
{{both=('%1%' == '%1'+'%')}}
-title "Jumping Rules!"
-desc "Your Strength determines how far you can jump.
{{'''\n**Long Jump**. When you make a long jump, you cover a number of feet up to your Strength score if you move at least 10 feet on foot immediately before the jump. When you make a standing long jump, you can leap only half that distance. Either way, each foot you clear on the jump costs a foot of movement.\n\nThis rule assumes that the height of your jump doesn’t matter, such as a jump across a stream or chasm. At your DM’s option, you must succeed on a DC 10 Strength (Athletics) check to clear a low obstacle(no taller than a quarter of the jump’s distance), such as a hedge or low wall. Otherwise, you hit it.\n\nWhen you land in difficult terrain, you must succeed on a DC 10 Dexterity (Acrobatics) check to land on your feet. Otherwise, you land prone.''' if (both or long) else ''}}
{{'''**High Jump**. When you make a high jump, you leap into the air a number of feet equal to 3 + your Strength modifier if you move at least 10 feet on foot immediately before the jump. When you make a standing high jump, you can jump only half that distance. Either way, each foot you clear on the jump costs a foot of movement. In some circumstances, your DM might allow you to make a Strength (Athletics) check to jump higher than you normally can.\n\nYou can extend your arms half your height above yourself during the jump. Thus, you can reach above you a distance equal to the height of the jump plus 1 1/2times your height.''' if (both or high) else ''}}"
{{f'-f "**Long Jump** (Standing)| {strength} feet ({strength/2} feet)"' if (both or long) else ''}}
{{f'-f "**High Jump** (Standing)| {3+strength} feet ({(3+strength)/2} feet)"' if (both or high) else ''}}
```