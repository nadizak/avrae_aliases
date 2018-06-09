## Eladrin's Fey Step
```GN
!servalias feystep embed
{{set("counter", "Fey Step")}}
{{create_cc_nx(counter, 0, "1", "short", "bubble")}}
{{mod_cc(counter, -1, True)}}
-title "<name> Teleports !"
-desc "As a bonus action, you can magically teleport up to 30 feet to an unoccupied space you can see. Once you use this trait, you can’t do so again until you finish a short or long rest.
When you reach 3rd level, your Fey Step gains an additional effect based on your season; if the effect requires a saving throw, the DC is {{8 + proficiencyBonus + charismaMod}}:
- **Autumn**: Immediately after you use your Fey Step, up to two creatures of your choice that you can see within 10 feet of you must succeed on a Wisdom saving throw or be charmed by you for 1 minute, or until you or your companions deal any damage to it.
- **Winter**: When you use your Fey Step, one creature of your choice that you can see within 5 feet of you before you teleport must succeed on a Wisdom saving throw or be frightened of you until the end of your next turn.
- **Spring**: When you use your Fey Step, you can touch one willing creature within 5 feet of you. That creature then teleports instead of you, appearing in an unoccupied space of your choice that you can see within 30 feet of you.
- **Summer**: Immediately after you use your Fey Step, each creature of your choice that you can see within 5 feet of you takes fire damage equal to your Charisma modifier (minimum of 1 damage)."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "MToF" -color <color> -thumb <image>
```