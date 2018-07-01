## DM Feedback
```GN
!servalias DMfeedback embed -title "How did the DM do?" -desc "Tell us here: https://docs.google.com/forms/d/e/1FAIpQLScpzi_CiLqG7hljj5NU3aIJ58N6SzGzfx8N0OVLe7ZLlJqNnw/viewform"
```

## Split Gold
```GN
!servalias gold embed
{{set("lootStr", "%1%")}}
{{set("pI", int(lootStr.find("pp")))}}
{{set("pp", int(lootStr[:pI] if pI!=-1 else 0))}}
{{set("lootStr", lootStr[pI+2 if pI!=-1 else 0:])}}
{{set("gI", int(lootStr.find("gp")))}}
{{set("gp", int(lootStr[:gI] if gI!=-1 else 0))}}
{{set("lootStr", lootStr[gI+2 if gI!=-1 else 0:])}}
{{set("sI", int(lootStr.find("sp")))}}
{{set("sp", int(lootStr[:sI] if sI!=-1 else 0))}}
{{set("lootStr", lootStr[sI+2 if sI!=-1 else 0:])}}
{{set("cI", int(lootStr.find("cp")))}}
{{set("cp", int(lootStr[:cI] if cI!=-1 else 0))}}
{{set("lootStr", lootStr[cI+2 if cI!=-1 else 0:])}}
{{set("numPlayers", %2%)}}
{{set("totalGp", pp*10+gp+(sp/10)+(cp/100))}}
{{set("perPlayer", totalGp/numPlayers)}}
{{set("currencyStrings", [])}}
{{0 if not pp else currencyStrings.append(str(pp)+" pp")}}
{{0 if not gp else currencyStrings.append(str(gp)+" gp")}}
{{0 if not sp else currencyStrings.append(str(sp)+" sp")}}
{{0 if not cp else currencyStrings.append(str(cp)+" cp")}}
-title "Total Gold"
-desc "{{" + ".join(currencyStrings)}} = {{totalGp}} gp"
-f "Number of Players|{{numPlayers}}"
-f "Gold Per Player|{{perPlayer}}"
-footer "1pp=10gp  1sp=0.1gp 1cp=0.01gp"
```

## Loot
**Credit to @silverbass#2407**
```GN
!servalias loot multiline
!embed {{set("rar","%1%".lower() if "%1" + "%" != "%1%" else "common")}}{{set("proper","Common" if rar[0:3] == "com" else "Uncommon" if rar[0:3] == "unc" else "Rare" if rar[0:3] == "rar" else "Very Rare" if rar[0:3] == "ver" else "Legendary" if rar[0:3] == "leg" else "ERROR")}} -title "Rolling for a {{proper}} Magic Item!" {{set("items", get_gvar("d3ae294a-f25d-4487-9300-6883cca339ce").split('\n')[1::] if rar[0:3] == "com" else get_gvar("cf95d38b-ce56-4687-8934-def1490c07b0").split('\n')[1::]+get_gvar("aa8a49a6-c9e0-4d0b-9fb2-fd91fa6c7f76").split('\n')[2::] if rar[0:3] == "unc" else get_gvar("e94e05aa-3ca5-4d64-aaf3-465f72396fa5").split('\n')[1::]+get_gvar("3555fb93-5d2f-46ee-b4ba-f876cae8db61").split('\n')[2::] if rar[0:3] == "rar" else get_gvar("41c18347-e4b1-4d9f-960d-9d8d6b5bf8c9").split('\n')[1::] if rar[0:3] == "ver" else get_gvar("be67dd4d-85c2-4078-aba8-f245ca97999a").split('\n')[1::] if rar[0:3] == "leg" else "")}}{{set("roll", vroll("1d48" if rar[0:3] == "com" else "1d96" if rar[0:3] == "unc" else "1d107" if rar[0:3] == "rar" else "1d72" if rar[0:3] == "ver" else "1d45" if rar[0:3] == "leg" else "0"))}} -desc "~~                                                                                                                                   ~~" -f "Roll | {{roll}}" -f "Loot| {{items[roll.total]}}" -footer "Awarding Magic Items | XGtE 139-145 & DMG 144-215" -color ede15e
!item {{items[roll.total]}}
```

## Weather
**Credit to @silverbass#2407 and @newtim#1227**
```GN
!servalias weather embed {{set("x","&1&")}}{{set("v",x not in "biomeslist")}}{{set("weather",get_gvar("ffc101ab-8284-4849-99fe-9f130b8b6027"))}}{{set("f",weather.lower().find(x.lower()) if x!="%1"+"%" else -1)}}{{set("f2",-1 if f<0 else 0 if f==0 else f if weather[f]=="\n" else 1+weather.rfind("\n",0,f) if f>0 else -1)}}{{set("dl",weather[f2:-1] if f!=-1 else weather)}}{{set("x2",dl.split("\n")[0])}}{{set("v",f!=-1)}}{{set("p",season if exists("season") and "%2%"=="%2"+"%" else "%2%")}}{{set("s",1 if p in "spring" else 2 if p in "summer" else 3 if p in "fallautumn" else 0)}}{{set("var",dl.split("\n")[1].split(" "))}}{{set("rain",dl.split("\n")[2].split(" "))}}{{set("wind",dl.split("\n")[3].split(" "))}}{{set("temp",dl.split("\n")[4].split(" "))}}{{set("th",roll(str(int(temp[s]))+"+"+var[0]))}}{{set("tl",roll(str(int(temp[s]))+"-"+var[0]))}}{{set("r",roll("1d20+"+rain[s]))}}{{set("w",max(0,roll(var[1]+"-"+var[1]+"+"+wind[s])))}}
{{set("wd",roll("1d8"))}}{{set("dir","North Northeast East Southeast South Southwest West Northwest".split(" "))}}
-title "{{"Today's Weather: "+x2+", "+("Winter" if s==0 else "Spring" if s==1 else "Summer" if s==2 else "Fall") if v else "Supported Biomes"}}"
{{"-f \"Weather| "+("? Snow" if r>21 and r<27 and tl<33 else "?? Blizzard" if r>26 and tl<33 else "? Clear" if r<16 else "?? Mostly Clear" if r<17 else "? Partly Cloudy" if r<19 else "?? Mostly Cloudy" if r<20 else "? Overcast" if r<21 else "?? Showers" if r<23 else "?? Downpour" if r<28 else "? Storm")+"\"" if v else ""}}
{{"-f \"Wind| ?? "+str(w)+" mph, "+(dir[wd-1] if w!=0 else "Still")+"\"" if v else ""}}
{{"-f \"Temperature| ?? **High:** "+str(th)+" °F | **Low**: "+str(tl)+" °F \"" if v else ""}}
{{"-desc \""+"\n".join(weather.split("\n")[::5])+"\"" if not v else ""}}
{{get_gvar("f70ae9ac-835a-47e4-bc6e-2c62667d49f2") if not v else ""}}
{{"-footer \"!weather list to see supported biomes and commands\"" if v else ""}} -color <color>


Emoji's are not preserved through common text editors and they will be lost if you copy and paste this snippet.
```