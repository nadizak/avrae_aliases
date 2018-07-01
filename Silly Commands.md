## Banhammer
```GN
!servalias banhammer embed 
{{set("attack", vroll("1d20+" + str(strengthMod+proficiencyBonus) + "+20[DM Privilege]"))}}
{{set("damage", vroll("4d12+10[Bludgeoning] + 6d8[Radiant] + 6d8[Fire] + 10d4[Psychic]"))}}
-title "*The Ban Hammer swiftly falls on the unjust and stupid*!" 
-desc "*This attack automatically hits if the target is a terrible person. The target is also vulnerable to the damage if everyone agrees that they deserve it.*

Regardless of whether it hits or not the target must make a Dex save (DC 25) or take half of the on hit damage and a fourth if they succeed.

Lastly they must make a Wisdom save (DC 25) or be paralyzed for 1 min. Nothing may remove this condition except DM intervention." 
-f "Attack|**To Hit:** {{attack}}"
-f "Damage|**To Hit:** {{damage}}"
-thumb <image> 
-color <color>
```

## Banhammer Ultimate
```GN
!servalias banhammer2 embed 
{{set("attack", vroll("1d20+" + str(strengthMod+proficiencyBonus) + "+20[DM Privilege]"))}}
{{set("damage", vroll("4d12+10[Bludgeoning] + 6d8[Radiant] + 6d8[Fire] + 10d4[Psychic]"))}}
-title "*The Ban Hammer swiftly falls on the unjust and stupid*!" 
-desc "*This attack automatically hits if the target is a terrible person. The target is also vulnerable to the damage if everyone agrees that they deserve it.*

Regardless of whether it hits or not the target must make a Dex save (DC 25) or take half of the on hit damage and a fourth if they succeed.

Lastly they must make a Wisdom save (DC 25) or be paralyzed for 1 min. Nothing may remove this condition except DM intervention." 
-f "Attack|**To Hit:** 1d20 (**20**) + 20 [DM Privilege] = 40"
-f "Damage|**To Hit:** 8d12 (**12**, **12**, **12**, **12**, **12**, **12**, **12**, **12**) + 10 [Bludgeoning] + 12d8 (**8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**) [Radiant] + 12d8 (**8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**, **8**) [Fire] + 20d4 (**4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**, **4**) [Psychic] = {{2*(12*4+10+6*8+6*8+10*4)}}"
-thumb <image> 
-color <color>
```


## Boop
```GN
!servalias boop embed 
{{set("attack", vroll("1d20+"+str(strengthMod+proficiencyBonus)))}}
-title "*Boop*!" 
-desc "*This attack deals no damage, and automatically hits if the target allows it.*" 
-f "Attack|**To Hit:** {{attack}}" 
-thumb <image> 
-color <color>
```

## Bap
```GN
!servalias bap embed 
{{set("attack", vroll("1d20+"+str(strengthMod+proficiencyBonus)))}}
-title "*Bap*!" 
-desc "*This attack deals no damage, and automatically hits if the target allows it.*" 
-f "Attack|**To Hit:** {{attack}}" 
-thumb <image> 
-color <color>
```
