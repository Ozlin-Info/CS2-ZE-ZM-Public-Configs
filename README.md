# CS2 ZE/ZM Server Public Configuation
Here you can find a list of public configuations for Ozlin Info game community server in Australia. 

https://steamcommunity.com/groups/ozlin-gaming

> [!NOTE]  
> The configurations here are provided "as-is" for our community and are not always 100% up to date. Feel free to use these configs if it works, but make sure you also pay it forward for other server owners and set your repo public!
>

## BossHP 
Empty folder, reserved for future. 

## Entwatch 
Using darkerz7's public EntWatch plugin https://github.com/darkerz7/EntWatchSharp

> [!WARNING]  
> Starting from 2025-06-27, our EntWatch config definition is changed to accept `HammerID`, `TriggerID`, `ButtonID`, and `MathID` with both String and Integer values. This is due to when the game engine decides to use string values.
> 
> New or updated configs here will be in String value by default.
 
**Example Structure**
```json[
	{
		"Name": "",					//String, FullName of Item (Chat)
		"ShortName": "",				//String, ShortName of Item (Hud)
		"Color": "",					//String, One of the colors. (Chat)
		"HammerID": "0",				//String or Integer, weapon_* HammerID
		"GlowColor": [0,0,0,0],				//Array[4], One of the colors. (Glow)
		"BlockPickup": false,				//Bool, The item cannot be picked up
		"AllowTransfer": false,				//Bool, Allow admins to transfer an item
		"ForceDrop": false,				//Bool, The item will be dropped if player dies or disconnects
		"Chat": false,					//Bool, Display chat items
		"Hud": false,					//Bool, Display Hud items
		"TriggerID": "0",				//String or Integer, Sets a trigger that an ebanned player cant activate, mostly to prevent picking up weapon_knife items
		"UsePriority": false,				//Bool, Enabled by default. You can disable the forced pressing of the button on a specific item
		"SpawnerID": 0,					//Integer, Allows admins to spawn items. Not recommended to use because it can break the items. Type point_template's HammerID which spawns the item
		"AbilityList": [				//Array of abilities
			{
				"Name": "",			//String, Custom ability name, can be omitted
				"ButtonID": "0",		//String or Integer, Allows you to sort buttons
				"ButtonClass": "",		//String, Button Class, Can use "game_ui" for anoter activation method
				"Filter": "",			//String, Filter value for activator. |$attribute| for filter_activator_attribute_int (starts with $); |context:value| for filter_activator_context (contains :); other for filter_activator_name
				"Chat_Uses": false,		//Bool, Display chat someone is using an item(if disabled chat)
				"Mode": 0,			//Integer, Mode for item. 0 = Can hold E, 1 = Spam protection only, 2 = Cooldowns, 3 = Limited uses, 4 = Limited uses with cooldowns, 5 = Cooldowns after multiple uses, 6 = Counter - stops when minimum is reached, 7 = Counter - stops when maximum is reached, 8 = Health button
				"MaxUses": 0,			//Integer, Maximum uses for modes 3, 4, 5
				"CoolDown": 0,			//Integer, Cooldown of item for modes 2, 4, 5
				"Ignore": false,		//Bool, Ignore item display
				"LockItem": false,		//Bool, Lock button/door/game_ui_IO
				"MathID": "0",			//String or Integer, math_counter HammerID for modes 6, 7
				"MathNameFix": false		//Bool, Fix the name of the math_counter (Work with flag: Preserve entity names (Don't do name fixup) ->point_template/env_entity_maker)
			},
			{
				"Name": "",
				"ButtonID": "0",
				"ButtonClass": "game_ui::PressedAttack",	//Example for Game_UI
				"Filter": "",
				"Chat_Uses": false,
				"Mode": 0,
				"MaxUses": 0,
				"CoolDown": 0,
				"Ignore": false,
				"LockItem": false,
				"MathID": "0",
				"MathNameFix": false
			}
		]
	},
	{
		"Name": <Next Item...>
	}
]
```

## Mapconfig 
Plugin from https://github.com/SlashPlayGG/MapConfigurator

You will be able to quickly and easily create unique configuration files on a per-map basis.

Order of cvar execution: prefixes -> MapName -> forced folder.

Everything in the `forced` folder are executed on every time the round starts. Only use this part if the map keeps overriding cvar.

## Map-Message 
Private plugin.

Regarding the map text translations in CS2, currently it can be done via stripper config (![example here](https://github.com/gflze/CS2-ZE-Configs/blob/main/stripper/ze_minecraft_sakura/default_ents.jsonc)). 

However, not everyone knows how to mess with stripper configs. So here we have ChatHud approaches back in CS:GO era. Once the map texts are generated in .json file, it can be edited and overridden the "default" field to display the English translation.

You may see this approach in Chinese CS2 zombie escape communities where they override English text to Chinese. And we are doing the opposite here.

**Example Structure**
```json
  "（僵尸10秒后传送 快跑(▽)）": { // Original text. Do not modify this line.
    "Translation": "(Zombies will teleport in 10 seconds, run! (▽))", // Overridden text to be displayed in game
    "M-Bool": false, // Reserved field for future implementation
    "Value": 0 // Reserved field for future implementation
  },
```

## RockTheVote 
Plugin modified by @oz-lin, from https://github.com/Oz-Lin/cs2-rockthevote 

Only the maplist.txt is available so you can see which maps are added/enabled/disabled/removed from our server. Disabled maps are commented out with double-slash notations //.

### Due to Steam Workshop approach for CS2, we have no control of the map repository as in CS:GO FastDL method. 
If the Workshop uploader decided to remove or hidden the map from Steam Workshop, or the map is removed due to copyright claims, we have no idea until the server changed to that specific map and encountered Workshop download error. Even if you subscribed and played that workshop map before, you still can't play it anymore.

### We mainly remove/disable maps from maplist.txt due to Workshop download error or material error in the map that crashes the client.
If you encounter Workshop download error, report to our Community Discord with your in-game console logs.

`[Client] Received S2C_CONNECTION from ip:port [addons:'3173223192,3157463861,3163629484']`
Here the first addon is the Workshop map ID. In case if it's taken down, you know which Workshop ID gives you error.

### Our message to mappers
In the workshop, you can actually continue to override the original upload to update the map, instead of deleting the original upload and reupload the new version.

If, for some reason, you want to change the name or version of the map uploaded to existing workshop, as long as the workshop ID remains unchanged, the map can still be recognised as usual, and the server and player client can also update the map status synchronously.

However, if you delete the original upload and re-releasing the new version, the workshop ID is inconsistent, and we cannot recognise the map normally. Even if players have subscribed to and played the old version of the map before, they will all encounter workshop download error when entering the server.

I hope you understand the Steam Workshop mechanism. Unlike the separate FastDL map repository back in the CS:GO era, the community server administrator and managers cannot track the map status in real time, unless an error is reported when entering the server.

## StripperCS2
Public Metamod plugin, available from https://github.com/Source2ZE/StripperCS2

Unfortunately there are no detailed instructions or tutorials about how to make Stripper config for CS2. We cannot provide adequate support if you are struggle with understanding the stripper structure. 

Config example from StripperCS2 readme
```
{
  "filter": [
    {
      // no terrorists >:(
      "classname": "info_player_terrorist"
    }
  ],

  "modify": [
    {
      "match":
      {
        "classname": "func_door_rotating",
        "io": [
          {
            "outputname": "OnFullyClosed"
          }
        ]
      },
      "replace":
      {
        "targetname": "yippe",
        "io":
        {
          "outputname": "OnClose"
        }
      },
      "insert":
      {
        "renderamt": "100",
        "io": [
          {
            "outputname": "OnFullyOpened",
            "inputname": "Lock",
            "targetname": "lockable_door"
          }
        ]
      },
      "delete":
      {
        "model": "models/bruh.mdl",
      }
    }
  ],

  "add": [
    {
      "classname": "func_button",
      "origin": "100 10 500"
      // ...
    }
  ],

  // Optional single object style, instead of using array
  "add": {
    "classname": "trigger_multiple",
    "origin": "500 80 1000"
    // ...
  }
}
```

## ZBuy Config (maybe)
Empty folder, reserved until we have a CounterStrikeSharp plugin to replace the CS2Fixes weapon purchase module.

We may have cvar configs for global/prefix/specific maps with variable grenade purchases limit.

## Update Frequency
Usually checked once a day during Sydney night time. Push/Pull updates are done manually until we find a way to automate on the server side. 

![Gametracker banner](https://cache.gametracker.com/server_info/139.99.144.28:28058/b_560_95_1.png)

## Acknowledgement 
Due to a shortage of hands in Australia/New Zealand, we recognise that Zombie Escape is a community effort and that there are other resources where you can get config files to make maps work better.
* GFL USA: https://github.com/gflze/CS2-ZE-Configs
* 93x China: https://github.com/UpKK-Xnet-YYDCS/UPKK_ZE_PUBLIC
* Looking for other contributors - we can credit you on this repository!
