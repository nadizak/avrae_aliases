## Reliable Talent
```python
!servsnippet talent -mc 10
```

## Sneak Attack
```python
!servsnippet sneak -d1 "{{ceil(int(RogueLevel)/2)}}d6 [Sneak Attack]"
```

## Stroke of Luck
```python
!servalias luck embed
{{set("lvl", int(RogueLevel))}}
{{set("counter", "Stroke of Luck")}}
{{mod_cc(counter, -1, True)}}
-title "<name> Has a Stroke of Luck!"
-desc "At 20th level, if your attack misses a target within range, you can turn the miss into a hit. Alternatively, if you fail an ability check, you can treat the d20 roll as a 20.

Once you use this feature, you can't use it again until you finish a short or long rest."
-f "{{counter}}|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Rogue | PHB 97" -color <color> -thumb <image>
```