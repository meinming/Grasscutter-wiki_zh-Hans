# 命令行

您可能希望使用手册生成命令(`java -jar grasscutter.jar -handbook`)在安装Grasscuter的终端中。
它将生成手册（GM-handbook.txt），在那里你可以找到敌人/物品等的ID。

您可能希望使用 gacha map生成程序 (`java -jar grasscutter.jar -gachamap`)来生成一个mapping file 为 gacha record subsystem. 
文件将生成在`(resources)/gcstatic`. (另外, 您可能只看到数字ID在gacha record page)

在每个玩家的好友列表中都有一个名为“Server”的虚拟用户，您可以发送消息以使用命令。
命令也适用于其他聊天室，例如私密/团队聊天。为了在游戏中运行命令, 您需要添加前缀 `/` 或者 `!` 在你的信息中 (例如： `/pos`)

### 目标
 1. 对于以玩家为目标的命令，您可以在任何位置指定带有“@UID”的目标UID作为参数。
 2. 如果您向另一个玩家（而不是“服务器”虚拟玩家）发送有效命令，如果您尚未设置目标，则他们将成为该命令的执行目标。
 3. 如果以上任何一项都不适用，它将默认为您以前使用：`/target<UID>`为执行目标。
 4. 如果上述 *都*  不适用，您将成为该命令的目标。如果您是从服务器控制台输入命令，**它将不工作**！

请注意，在其他玩家上执行命令通常需要相应的权限。 
（例如，“player.give”如果用于其他玩家，则变为“player.give.others”）

您可以使用'@'作为参数来设置覆盖步骤2-4的空目标。目前，这用于特例`sendmessage` ，该命令发送给服务器上的*所有* 在服务器上的玩家, 作用就像过时的 `broadcast` 命令。

### 信息命令（无需权限）
| 命令     | 描述                                   | 缩写 | 目标     | 用法           |
| -------- | -------------------------------------- | ---- | -------- | -------------- |
| list     | 列出在线玩家。                         |      | 无       | list           |
| help     | 发送帮助消息或显示有关指定命令的信息。 |      | 无       | help [command] |
| position | 发送你当前的坐标。                     | pos  | 在线玩家 | position       |

### 服务器管理员的命令
| 命令    | 描述                                                                               | 缩写 | 目标     | 用法                                     | 所需权限                     |
| ----------- | ----------------------------------------------------------------------------------------- | ----- | ------------- | ------------------------------------------- | ------------------ |
| account     | 使用指定的用户名和游戏内UID（如果指定）创建帐户 |       | 仅服务端 | `account <create\|delete> <username> [UID]` | (只能在服务端控制台上使用) |
| permission  | 授予或删除用户的权限                                     |       | 玩家        | `permission <add\|remove> <permission>`     | permission |
| kick        | 将指定的玩家踢出服务器                                   | k     | 在线玩家 | `kick`                                      | server.kick (仅适用于其他人) |
| ban         | 从服务器踢和禁止指定的玩家                        |       | 玩家        | `ban [timestamp] [reason]`                  | server.ban         |
| unban       | 从服务器解除禁止指定的玩家                                      |       | 玩家        | `unban`                                     | server.ban         |
| sendmessage | 向作为服务器的玩家发送消息。如果在没有目标的情况下使用，向所有玩家发送消息。 | say   | 无          | `say <message>`                             | server.sendmessage |
| reload      | 重新加载服务器配置                                                      |       | 无          | `reload`                                    | server.reload      |
| stop        | 停止服务端                                                                  |       | 无          | `stop`                                      | server.stop        |

### 可能伤害玩家的命令
| 命令           | 描述                                                         | 缩写               | 目标     | 用法                                  | 所需权限                  |
| -------------- | ------------------------------------------------------------ | ------------------ | -------- | ------------------------------------- | ------------------------- |
| clear          | 从库存中删除所有未装备和未锁定的lv10工件(art)/武器(wp)/材料(mat) |                    | 在线玩家 | `clear <all\|wp\|art\|mat>`           | player.clearinv           |
| give           | 将(一件)物品提供给您或指定的玩家。                           | g item giveitem    | 在线玩家 | `give <itemId\|avatarId> [see below]` | player.give               |
| resetconst     | 将当前选定（或全部）字符重置为C0。重新记录来查看正确的效果。 | resetconstellation | 在线玩家 | `resetconst [all]`                    | player.resetconstellation |
| setfetterlevel | 设置当前选定角色的好感度                                     | setfetterlvl       | 在线玩家 | `setfetterlevel <level>`              | player.setfetterlevel     |
| setprop        | 设置accountwide属性。                                        | prop               | 在线玩家 | `setprop <prop> <value>`              | player.setprop            |
| talent         | 设置当前选定角色的天赋级别                                   |                    | 在线玩家 | `talent <talentID> <value>`           | player.settalent          |

### 没有持久效果的命令
| 命令         | 描述                                            | 缩写  | 目标          | 用法                                                         | 所需命令            |
| ------------ | ----------------------------------------------- | ----- | ------------- | ------------------------------------------------------------ | ------------------- |
| oop          | 强迫某人加入他人的世界。                        |       | 在线玩家      | `coop [host UID (default self)]`                             | server.coop         |
| tpall        | 将你世界中的所有玩家传送到你的位置。            |       | 在线玩家      | `tpall`                                                      | player.tpall        |
| heal         | 治疗当前队伍中的所有角色。                      | h     | 在线玩家      | `heal`                                                       | player.heal         |
| killall      | 杀死当前场景或相应玩家的指定场景中的所有实体。  |       | 在线玩家      | `killall [sceneId]`                                          | server.killall      |
| setstats     | 设置当前选定角色的状态。                        | stats | Online Player | `setstats <stat> <value>`                                    | player.setstats     |
| spawn        | 在你周围产生一些实体。                          |       | 在线玩家      | `spawn <entityId\|itemId> [amount] [level(monster only)]`    | server.spawn        |
| team         | 在当前团队中添加、删除或交换化身。索引从1开始。 |       | 在线玩家      | `team <add\|remove\|set> [avatarId,...] [index\|index-index,...]` | player.team         |
| teleport     | 改变玩家的位置。                                | tp    | 在线玩家      | `teleport <x> <y> <z> [sceneId]`                             | player.teleport     |
| enterdungeon | 按秘境ID输入秘境。                              |       | 在线玩家      | `enterdungeon <dungeon id>`                                  | player.enterdungeon |
| weather      | 改变天气                                        | w     | 在线玩家      | `weather [weatherID] [climate]`                              | player.weather      |

### Give 命令
`give`命令现在具有旧的`giveall`、`giveart`和`givechar`命令的功能。

`give`有关键字参数`x<amount>`、`lv<level>`、`r<refineration>`和“`c<constellation>`，它们可以在命令中的任何位置使用，就像“@UID”一样。
`x<amount>`也可以写为`<amount>x`，`lv<level>`可以是` 1<level>`或` lv1<level>`，它们都可以无空格链接在一起，例如` lv90r5x10`。

要给所有物品，请执行 `give <all|weapons|mats|avatars> [x<amount>]`. 上述关键字参数对此都有效。

The artifact syntax is `give <artifactId> [mainPropId] [<appendPropId>[,<times>]]...`. 使用`x<amount>` 和 `lv<level>` 时，注意它使用0-20的级别来匹配游戏中显示的数字，而不是1-21，但尽管如果你给它输入`v21`，它也不会报错。

### SetProp 命令
`prop <godmode|nostamina|unlimitedenergy> <on|off|toggle|1|0>` 代替了过时的`godmode`, `nostamina`, `unlimitenergy` 命令.

`prop <god|ns|ue> <value>` 是它们最短的缩写.

`prop abyss 12` 代替了 `unlocktower`. 完整的语法是 `prop <abyss|abyssfloor|ut|tower|towerlevel|unlocktower> <floor to unlock>` 

去设置battlepass等级: `prop <bplevel|bp|battlepass> <level>`

设置世界等级: `prop <worldlevel|wl> <level>`

AR: `prop player_level <level>`