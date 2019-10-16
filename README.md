# ChildToNPC
This is a Stardew Valley mod called Child To NPC. Child To NPC is a modding tool which converts children into full-fledged NPCs, allowing them to be patched by other mods in the sames ways that NPCs can. This mod is newly released, so please let me know if you run into any issues using it.

## How to use:

The main purposes of Child To NPC is to make Content Patcher packs possible, so I recommend you look over the links below for instructions on how to make Content Patcher packs editing NPCs. (I'd also recommend looking over some of the Custom NPC mods that are already out there.)

The Readme for Content Patcher, which explains how to make Content Patcher packs:
https://github.com/Pathoschild/StardewMods/blob/9c5d557b9591721ea34dd162da25e21c19b22ba0/ContentPatcher/README.md

The page from the Stardew Valley Wiki about NPC data:
https://stardewvalleywiki.com/Modding:NPC_data

MissCoriel's template for making Content Patcher NPC mods:
https://www.nexusmods.com/stardewvalley/mods/3446

Once you feel comfortable with making Content Patcher mods for NPCs, then you're ready to mod!

(Also, remember to download Spacechase0's Custom NPC Fixes to avoid schedule issues for NPCs: 
https://www.nexusmods.com/stardewvalley/mods/3849)

## Custom Tokens for Content Patcher
### Manifest.json
Inside the manifest.json, be sure that you list "Loe2run.ChildToNPC" as a required dependency. Not only does this allow Child To NPC to run first when generating NPCs, but it also allows you to make use of the Content Patcher tokens this mod creates.

### Tokens
Child To NPC makes use of the Content Patcher API to create custom tokens. These tokens take the form of:
```cs
{{Loe2run.ChildToNPC/<Token Name Here>}}
```

#### Name
```cs
{{Loe2run.ChildToNPC/FirstChildName}}
```
This is the token you will use the most. It gives you access to the name of the NPC, so wherever you would normally use an NPC's name, like in a Target field, you can instead put this token.

Here's an example entry from your content.json:
```cs
{
  "LogName": "Child Portraits",
  "Action": "Load",
  "Target": "Portraits/{{Loe2run.ChildToNPC/FirstChildName}}",
  "FromFile": "assets/FirstChildPortrait.png"
},
```
#### Birthday
```cs
{{Loe2run.ChildToNPC/FirstChildBirthday}}
```
This token returns the child's birthday in the form of "day season year". For example, you can use this value when creating the NPC Disposition.

```cs
{
  "LogName": "Child NPC Dispositions",
  "Action": "EditData",
  "Target": "Data/NPCDispositions",
  "Entries": {
    "{{Loe2run.ChildToNPC/FirstChildName}}": ".../{{Loe2run.ChildToNPC/FirstChildBirthday}}/..."
  }
},
```

#### Gender
```cs
{{Loe2run.ChildToNPC/FirstChildGender}}
```
This token returns the child's gender in the form of the string "male" or "female". This is also useful for the NPC Disposition, or as a condition.
```cs
{
    "LogName": "Child Portraits",
    "Action": "Load",
    "Target": "Portraits/{{Loe2run.ChildToNPC/FirstChildName}}",
    "FromFile": "assets/Image/FirstSon.png",
    "When": {
        "{{Loe2run.ChildToNPC/FirstChildGender}}": "male"
    }
},
```

#### Bed Location
```cs
{{Loe2run.ChildToNPC/FirstChildBed}}
```
```cs
{{Loe2run.ChildToNPC/FirstChildBed:7 7}}}
```
This token by default returns a tile position in the form of "x y" where the child will go to bed. It's generated in the same way that Family Planning generates bed spots, so that if there are more than two children, they will share beds. 

This token also takes input if you'd like to choose where your child goes to bed, as you'll see above.

#### TODO
I'm in the process of adding more tokens, like parent identities.

## How to Uninstall
To uninstall ChildToNPC, all you have to do is remove the ChildToNPC mod (and the other associated CP mods) from your mod folder. I've designed ChildToNPC so NPCs never get saved with the save data, so you shouldn't run into any issues when you get rid of them.
(If you do run into a bug which corrupts your save data, please let me know!)

## Final Notes
This mod uses Harmony, so it could run into issues with other mods which patch the same methods. If you notice any issues, let me know!

This mod is currently only compatible with singleplayer.

If you have questions about anything, feel free to get in contact with me! One of the best ways to talk to me is through the Stardew Valley Discord. I'm Loe#4013 there. https://stardewvalleywiki.com/Modding:Community#Discord
