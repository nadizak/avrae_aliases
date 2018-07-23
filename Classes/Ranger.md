## All in One Ranger Alias
```python
!alias ranger embed
{{d=load_json(get_gvar("f10bcbd4-1dec-4f3b-86c1-2b54c3ba465f"))}}
{{q="&*&".replace(" ","").lower()}}
{{set("o",(d[k] if (q in d and not set("k", q)) or ([set("k", k) for k in d.keys() if q and q in k]) else d.D))}}
-title "{{f'{name} uses {o.n}' if 'n' in o else o.t if 't' in o else ''}}"
-desc "{{o.d if 'd' in o else ''}}"
```

## Global Variable
```json
{
  "D": {
    "t": "Ranger",
    "d": "Primeval Awareness: `!ranger prim`\nHide in Plain Sight: `!ranger hide`\nVanish: `!ranger vanish`\n\n**Beast Master**\nExceptional Training: `!ranger train`\nBestial Fury: `!ranger fury`\n\n**Gloom Stalker**\nDread Ambusher: `!ranger ambush`\nShadowy Dodge: `!ranger shado`\n\n**Horizon Walker**\nDetect Portal: `!ranger detect`\nPlanar Warrior: `!ranger war`\nEthereal Step: `!ranger step`\nDistant Strike: `!ranger dist`\nSpectral Defense: `!ranger defen`\n\n**Hunter**\nGiant Killer: `!ranger giant`\nHorde Breaker: `!ranger horde`\nVolley: `!ranger vol`\nWhirlwind Attack: `!ranger whirl`\nStand Against the Tide: `!ranger stand`\nUncanny Dodge: `!ranger dodge [damage]`\n\n**Monster Slayer**\nHunter's Sense: `!ranger sense`\nSlayer's Prey: `!ranger prey`\nMagic-User's Nemesis: `!ranger nemes`\nSlayer's Counter: `!ranger counter`\n"
  },
  "primevalawareness": {
    "n": "Primeval Awareness",
    "d": "You can use your action and expend one ranger spell slot to focus your awareness on the region around you. For 1 minute per level of the spell slot you expend, you can sense whether the following types of creatures are present within 1 mile of you (or within up to 6 miles if you are in your favored terrain): aberrations, celestials, dragons, elementals, fey, fiends, and undead. This feature doesn't reveal the creatures' location or number.",
    "s": "min"
  },
  "hideinplainsight": {
    "n": "Hide in Plain Sight",
    "d": "You can spend 1 minute creating camouflage for yourself. You must have access to fresh mud, dirt. plants. soot. and other naturally occurring materials with which to create your camouflage.\n\nOnce you are camouflaged in this way, you can try to hide by pressing yourself up against a solid surface, such as a tree or wall, that is at least as tall and wide as you are. You gain a +10 bonus to Dexterity (Stealth) checks as long as you remain there without moving or taking actions. Once you move or take an action or a reaction, you must camouflage yourself again to gain this benefit."
  },
  "vanish": {
    "n": "Vanish",
    "d": "You can use the Hide action as a bonus action on your turn. Also, you can't be tracked by non-magical means, unless you choose to leave a trail."
  },
  "exceptionaltraining": {
    "n": "Exceptional Training",
    "d": "On any of your turns when your beast companion doesn't attack, you can use a bonus action to command the beast to take the Dash, Disengage, Dodge, or Help action on its turn."
  },
  "bestialfury": {
    "n": "Bestial Fury",
    "d": "When you command your beast companion to take the Attack action, the beast can make two attacks, or it can take the Multi-attack action if it has that action."
  },
  "dreadambusher": {
    "n": "Dread Ambusher",
    "d": "At the start of your first turn of each combat, your walking speed increases by 10 feet, which lasts until the end of that turn. If you take the Attack action on that turn, you can make one additional weapon attack as part of that action. If that attack hits, the target takes an extra 1d8 damage of the weapon's damage type."
  },
  "shadowydodge": {
    "n": "Shadowy Dodge",
    "d": "Whenever a creature makes an attack roll against you and doesn't have advantage on the roll, you can use your reaction to impose disadvantage on it. You must use this feature before you know the outcome of the attack roll. "
  },
  "detectportal": {
    "n": "Detect Portal",
    "d": "As an action, you detect the distance and direction to the closest planar portal within 1 mile of you.\n\nOnce you use this feature, you can’t use it again until you finish a short or long rest.",
    "c": 1
  },
  "planarwarrior": {
    "n": "Planar Warrior",
    "d": "As a bonus action, choose one creature you can see within 30 feet of you. The next time you hit that creature on this turn with a weapon attack, all damage dealt by the attack becomes force damage, and the creature takes an extra r1 force damage from the attack."
  },
  "etherealstep": {
    "n": "Ethereal Step",
    "d": "As a bonus action, you can cast Etherealness with this feature, without expending a spell slot, but the spell ends at the end of the current turn.\n\nOnce you use this feature, you can’t use it again until you finish a short or long rest.",
    "c": 1
  },
  "distantstrike": {
    "n": "Distant Strike",
    "d": "When you take the Attack action, you can teleport up to 10 feet before each attack to an unoccupied space you can see.\n\nIf you attack at least two different creatures with the action, you can make one additional attack with it against a third creature."
  },
  "spectraldefense": {
    "n": "Spectral Defense",
    "d": "When you take damage from an attack, you can use your reaction to give yourself resistance to all of that attack’s damage on this turn.",
    "e": 1
  },
  "giantkiller": {
    "n": "Giant Killer",
    "d": "When a Large or larger creature within 5 feet of you hits or misses you with an attack, you can use your reaction to attack that creature immediately after its attack, provided that you can see the creature."
  },
  "hordebreaker": {
    "n": "Horde Breaker",
    "d": "Once on each of your turns when you make a weapon attack, you can make another attack with the same weapon against a different creature that is within 5 feet of the original target and within range of your weapon."
  },
  "volley": {
    "n": "Volley",
    "d": "You can use your action to make a ranged attack against any number of creatures within 10 feet of a point you can see within your weapon's range. You must have ammunition for each target, as normal, and you make a separate attack roll for each target."
  },
  "whirlwindattack": {
    "n": "Whirlwind Attack",
    "d": "You can use your action to make a melee attack against any number of creatures within 5 feet of you. with a separate attack roll for each target."
  },
  "standagainstthetide": {
    "n": "Stand Against the Tide",
    "d": "When a hostile creature misses you with a melee attack, you can use your reaction to force that creature to repeat the same attack against another creature (other than itself) of your choice."
  },
  "uncannydodge": {
    "n": "Uncanny Dodge",
    "d": "When an attacker that you can see hits you with an attack, you can use your reaction to halve the attack's damage against you.",
    "h": 1
  },
  "hunterssense": {
    "n": "Hunter's Sense",
    "d": "As an action, choose one creature you can see within 60 feet of you. You immediately learn whether the creature has any damage immunities, resistances, or vulnerabilities and what they are. If the creature is hidden from divination magic, you sense that it has no damage immunities, resistances, or vulnerabilities.\n\nYou can use this feature a number of times equal to your Wisdom modifier (minimum of once). You regain all expended uses of it when you finish a long rest.",
    "c": 1
  },
  "slayersprey": {
    "n": "Slayer's Prey",
    "d": "As a bonus action, you designate one creature you can see within 60 feet of you as the target of this feature. The first time each turn that you hit that target with a weapon attack, it takes an extra 1d6 damage from the weapon.\n\nThis benefit lasts until you finish a short or long rest. It ends early if you designate a different creature.",
    "c": 1
  },
  "magicusersnemesis": {
    "n": "Magic-User's Nemesis",
    "d": "When you see a creature casting a spell or teleporting within 60 feet of you, you can use your reaction to try to magically foil it. The creature must succeed on a Wisdom saving throw against your spell save DC, or its spell or teleport fails and is wasted.\n\nOnce you use this feature, you can’t use it again until you finish a short or long rest.",
    "dc": 1
  },
  "slayerscounter": {
    "n": "Slayer's Counter",
    "d": "If the target of your Slayer’s Prey forces you to make a saving throw, you can use your reaction to make one weapon attack against the quarry. You make this attack immediately before making the saving throw. If your attack hits, your save automatically succeeds, in addition to the attack’s normal effects."
  }
}
```