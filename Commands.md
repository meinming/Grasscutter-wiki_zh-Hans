# 命令行

您可能希望使用手册生成命令(`java -jar grasscutter.jar -handbook`)在安装Grasscuter的终端中。
它将生成手册（GM-handbook.txt），在那里你可以找到敌人/物品等的ID。

You may want to use the gacha map generation (`java -jar grasscutter.jar -gachamap`) to generate a mapping file for the gacha record subsystem. 
The file will be generated in `(resources)/gcstatic`. (otherwise, you may only see number IDs on the gacha record page)

在每个玩家的好友列表中都有一个名为“Server”的虚拟用户，您可以发送消息以使用命令。
命令也适用于其他聊天室，例如私密/团队聊天。为了在游戏中运行命令, 您需要添加前缀 `/` 或者 `!` 在你的信息中 (例如： `/pos`)

### Targeting
 1. 对于以玩家为目标的命令，您可以在任何位置指定带有“@UID”的目标UID作为参数。
 2. 如果您向另一个玩家（而不是“服务器”虚拟玩家）发送有效命令，如果您尚未设置目标，则他们将成为该命令的执行目标。
 3. 如果以上任何一项都不适用，它将默认为您以前使用：`/target<UID>`为执行目标。
 4. 如果上述 *都*  不适用，您将成为该命令的目标。如果您是从服务器控制台输入命令，**它将不工作**！

请注意，在其他玩家上执行命令通常需要相应的权限。 
（例如，“player.give”如果用于其他玩家，则变为“player.give.others”）

您可以使用'@'作为参数来设置覆盖步骤2-4的空目标。目前，这用于特例`sendmessage` ，该命令发送给服务器上的*所有* 在服务器上的玩家, 作用就像过时的 `broadcast` 命令。

### Informational commands (no permissions)
| Commands | Description                                                            | Alias | Targeting     | Usage          |
| -------- | ---------------------------------------------------------------------- | ----- | ------------- | -------------- |
| list     | Lists online players.                                                  |       | None          | list           |
| help     | Sends the help message or shows information about a specified command. |       | None          | help [command] |
| position | Sends your current coordinates.                                        | pos   | Online Player | position       |

### Commands for server admins
| Commands    | Description                                                                               | Alias | Targeting     | Usage                                       | Permission node    |
| ----------- | ----------------------------------------------------------------------------------------- | ----- | ------------- | ------------------------------------------- | ------------------ |
| account     | Creates an account with the specified username, and the in-game UID if specified.         |       | Server only   | `account <create\|delete> <username> [UID]` | (can only use on server console) |
| permission  | Grants or removes a permission for a user.                                                |       | Player        | `permission <add\|remove> <permission>`     | permission         |
| kick        | Kicks the specified player from the server.                                               | k     | Online Player | `kick`                                      | server.kick (only for others) |
| ban         | Kicks and bans the specified player from the server.                                      |       | Player        | `ban [timestamp] [reason]`                  | server.ban         |
| unban       | Unbans specified player from the server.                                                  |       | Player        | `unban`                                     | server.ban         |
| sendmessage | Sends a message to a player as the server. If used without a target, message all players. | say   | None          | `say <message>`                             | server.sendmessage |
| reload      | Reloads the server config.                                                                |       | None          | `reload`                                    | server.reload      |
| stop        | Stops the server.                                                                         |       | None          | `stop`                                      | server.stop        |

### Commands that can potentially harm players
| Commands       | Description                                                                                       | Alias              | Targeting     | Usage                                 | Permission node           |
| -------------- | ------------------------------------------------------------------------------------------------- | ------------------ | ------------- | ------------------------------------- | ------------------------- |
| clear          | Deletes all unequipped and unlocked lvl0 artifacts(art)/weapons(wp)/material(mat) from inventory. |                    | Online Player | `clear <all\|wp\|art\|mat>`           | player.clearinv           |
| give           | Gives item(s) to you or the specified player.                                                     | g item giveitem    | Online Player | `give <itemId\|avatarId> [see below]` | player.give               |
| resetconst     | Resets currently selected (or all) character(s) to C0. Relog to see proper effects.               | resetconstellation | Online Player | `resetconst [all]`                    | player.resetconstellation |
| setfetterlevel | Sets the friendship level for your currently selected character.                                  | setfetterlvl       | Online Player | `setfetterlevel <level>`              | player.setfetterlevel     |
| setprop        | Sets accountwide properties.                                                                      | prop               | Online Player | `setprop <prop> <value>`              | player.setprop            |
| talent         | Sets talent level for your currently selected character                                           |                    | Online Player | `talent <talentID> <value>`           | player.settalent          |

### Commands without lasting effects
| Commands     | Description                                                                             | Alias | Targeting     | Usage                                                             | Permission node     |
| ------------ | --------------------------------------------------------------------------------------- | ----- | ------------- | ----------------------------------------------------------------- | ------------------- |
| coop         | Forces someone to join the world of others.                                             |       | Online Player | `coop [host UID (default self)]`                                  | server.coop         |
| tpall        | Teleports all players in your world to your position.                                   |       | Online Player | `tpall`                                                           | player.tpall        |
| heal         | Heals all characters in your current team.                                              | h     | Online Player | `heal`                                                            | player.heal         |
| killall      | Kills all entities in the current scene or specified scene of the corresponding player. |       | Online Player | `killall [sceneId]`                                               | server.killall      |
| setstats     | Sets a stat for your currently selected character.                                      | stats | Online Player | `setstats <stat> <value>`                                         | player.setstats     |
| spawn        | Spawns some entities around you.                                                        |       | Online Player | `spawn <entityId\|itemId> [amount] [level(monster only)]`         | server.spawn        |
| team         | Add, remove, or swap avatars in your current team. Index start from 1.                  |       | Online Player | `team <add\|remove\|set> [avatarId,...] [index\|index-index,...]` | player.team         |
| teleport     | Change the player's position.                                                           | tp    | Online Player | `teleport <x> <y> <z> [sceneId]`                                  | player.teleport     |
| enterdungeon | Enter a dungeon by dungeon ID.                                                          |       | Online Player | `enterdungeon <dungeon id>`                                       | player.enterdungeon |
| weather      | Changes the weather.                                                                    | w     | Online Player | `weather [weatherID] [climate]`                                   | player.weather      |

### Give command
The `give` command now has the functionality of the old `giveall`, `giveart` and `givechar` commands.

`give` has keyword arguments `x<amount>`, `lv<level>`, `r<refinement>` and `c<constellation>` which can be used anywhere in the command, just like `@UID` can be.
`x<amount>` can also be written as `<amount>x`, and `lv<level>` can be `l<level>` or `lvl<level>`, and they can all be chained together without spaces, e.g. `lv90r5x10`.

To give all items, do `give <all|weapons|mats|avatars> [x<amount>]`. The above keyword arguments are all valid for this.

The artifact syntax is `give <artifactId> [mainPropId] [<appendPropId>[,<times>]]...`. `x<amount>` and `lv<level>` work with this, and note that this uses levels of 0-20 to match displayed in-game numbers rather than 1-21, though it won't complain if you feed it `lv21`.

### SetProp command
`prop <godmode|nostamina|unlimitedenergy> <on|off|toggle|1|0>` replaces the old `godmode`, `nostamina`, `unlimitenergy` commands.

`prop <god|ns|ue> <value>` are the shortest aliases for them.

`prop abyss 12` replaces `unlocktower`. Full syntax is `prop <abyss|abyssfloor|ut|tower|towerlevel|unlocktower> <floor to unlock>` 

To set BP level: `prop <bplevel|bp|battlepass> <level>`

And world level: `prop <worldlevel|wl> <level>`

AR: `prop player_level <level>`