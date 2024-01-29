> # PalWorld-Save-Movement-Complete-Tutorial
>
> Anyone is welcome to translate this tutorial into other languages.

# 幻兽帕鲁存档转移完全教程

> ### :warning: 
>
> 此转移操作可能会导致你的存档出现如下问题：  
> - 被暗巫猫带走。  
> - 被炸弹鸟炸掉。
>  
> 我仍然强烈建议你在进行任何操作之前进行充分的备份。防患于未然最重要。保持乐观和平和的心态，同时做好最坏的准备。跟着我一步一步完成这项工作。

## 前言

本教程面向那些拥有探索精神、一定的计算机技术经验，并且最重要的——具备耐心的玩家。我将一步步引导你完成幻兽帕鲁存档的转移过程。

## 准备工作

在开始之前，请确保你已经准备好以下几项：

1. 老主机的存档 - 你需要从你的老主机中获取幻兽帕鲁的存档文件。这是转移过程中不可或缺的一部分。

2. 新云服务器 - 准备一个新的云服务器，用于存放和运行幻兽帕鲁的新存档。

3. 存档文件位置 - 在你的服务器文件夹下找到 `Pal\Saved\SaveGames\<random_numbers>` 路径，保存。个人建议将整个 `Saved` 文件夹打包，以便进行未来的操作。

4. 下载压缩包 - 我会提供一个打包好的压缩包，里面包含了进行存档转移所需的所有必要文件。

5. 解压到合适位置 - 将压缩包解压到一个合适的位置。例如，你可以创建一个名为 `mirage_save` 的文件夹，用于存放解压后的文件。

6. 确认你现有的存档的服务端

   - LinuxServer Manual Install with Official Guide
   - LinuxServer 服务商面板服
   - WinServer 与 steamcmd
   - WinServer 与 steamclient
   - Windows 合作模式

请确保以上步骤都已经完成，然后我们可以继续下一部分的内容。

## 确定自己的存档玩家PID来源

PalWorld 的玩家 PID 依照两点来确定（我的未证实的经验）

1. 玩家的 steamID，个人资料的 ID

2. **服务器的 APPID**（重点）

   >  APPID 可以看服务端的 Output，会输出 `SteamAPPID = <NUMBER>`

   - 对于 Windows 用户来说，你们有三种 APPID
     - 未加载 steam 库导致的无 ID
     - steamcmd 安装独立客户端的 ID = 1623730
     - steamclient 安装独立客户端的 ID = 2394010
     - 合作模式的 ID = 2394010
   - 对于 Linux 用户来说，你们有两种 APPID
     - 未加载 steamclient.so 导致的无ID
     - 按照官方教程安装的 ID = 2394010

## 服务器 APPID 类型

- 无 ID

- 1623730 = 幻兽帕鲁游戏

- 2394010 = 幻兽帕鲁独立服务器

  >  :warning: 报告显示 1623730 与 2394010 会产生相同的效果，也就是其可以等价。

## 服务器间的转移

1. 确定自己转移前后的服务器 APPID 保持不变。（其中16与23相当）

2. 登录服务器以创建一个新世界。

3. **关闭服务器。**

4. 删除 `PalServer\Pal\Saved\SaveGames\0\`

5. - 对于Linux：  
     在 `PalServer\Pal\Saved\Config\LinuxServer\GameUserSettings.ini` 文件中，更改 以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。
   - 对于Windows：  
     在 `PalServer\Pal\Saved\Config\WindowsServer\GameUserSettings.ini` 文件中，更改 以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。

6. 将你的存档复制到 `PalServer\Pal\Saved\SaveGames\0\` 下。

   > 类似 `PalServer\Pal\Saved\SaveGames\0\\<your_save_here>\`

7. 删除 `PalServer\Pal\Saved\SaveGames\0\<your_save_here>\WorldOption.sav` （**可能没有，非常正常，没有不需要删除**）以允许修改 `PalWorldSettings.ini` 。（会导致玩家丢失地图以及重生点）

8. 登录服务器，验证是否转移成功，如果转移不成功，回到[确定自己的存档玩家 PID 来源](#确定自己的存档玩家PID来源)。

存档应该正常迁移了。

## 从合作模式迁移到服务器

合作模式与服务器间的转移最大的区别是有关主机存档的迁移。对于合作模式来说，主机玩家在本地存档里的ID是 `00000000000000000000000000000001.sav` 。

于是帕鲁 Discord 有大神写了一个 python 脚本，用来转换存档。地址如下：

[幻兽帕鲁主机存档修复](https://github.com/xNul/palworld-host-save-fix)

步骤如下：

### 在开始之前

1. 从 Github 下载 python 脚本，[palworld-host-save-fix](https://github.com/xNul/palworld-host-save-fix)，在我打包的文件中也有。
2. 安装 python > 3.10
3. 获取 [uesave-rs](https://github.com/trumank/uesave-rs)，在我打包的文件中也有，名字叫 uesave.exe。

### python脚本说明

> :cactus: GUID = PID 的十六进制版本，存档文件的文件名是 GUID

Command: 命令：
```
python fix-host-save.py <uesave.exe> <save_path> <new_guid> <old_guid>
```

> `<uesave.exe>` - uesave.exe 的路径  
> `<save_path>` - 保存文件夹的路径  
> `<new_guid>` - 新服务器上Player的 GUID  
> `<old_guid>` - 旧服务器中Player的 GUID

Example: 例：
```
python fix-host-save.py "C:\Users\John\.cargo\bin\uesave.exe" "C:\Users\John\Desktop\my_temporary_folder\2E85FD38BAA792EB1D4C09386F3A3CDA" 6E80B1A6000000000000000000000000 00000000000000000000000000000001
```

> 此脚本的作用是将一个 `GUID.sav` 迁移到另一个 `GUID.sav`，同时修改 `Level.sav` 以保证数据一致性。

### 开始

#### PART I:

1. 确定自己转移前后的服务器 APPID 保持不变。

2. 登录服务器以创建一个新世界。

3. **关闭服务器。**

4. 删除 `PalServer\Pal\Saved\SaveGames\0\`

6. - 对于Linux：  
     在 `PalServer\Pal\Saved\Config\LinuxServer\GameUserSettings.ini` 文件中，更改以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。
   - 对于Windows：  
     在 `PalServer\Pal\Saved\Config\WindowsServer\GameUserSettings.ini` 文件中，更改以 `DedicatedServerName` 匹配保存的文件夹名称。例如，如果保存的文件夹名称为 `2E85FD38BAA792EB1D4C09386F3A3CDA` ，则 `DedicatedServerName` 更改为 `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA` 。

7. 将你的存档复制到 `PalServer\Pal\Saved\SaveGames\0\` 下。

   > 类似 `PalServer\Pal\Saved\SaveGames\0\\<your_save_here>\`

8. 删除 `PalServer\Pal\Saved\SaveGames\0\<your_save_here>\WorldOption.sav` （**可能没有，非常正常，没有不需要删除**）以允许修改 `PalWorldSettings.ini` 。（会导致玩家丢失地图以及重生点）

9. **请让你的朋友登录服务器，验证是否转移成功，如果转移不成功，回到[确定自己的存档玩家 PID 来源](#确定自己的存档玩家PID来源)。**

#### PART II

1. 如果成功，现在开始解决你的作为主机的存档问题。

2. 请你登录服务器，创建角色，并开启一个存档点。

3. 这时候你可以看到在 `PalServer\Pal\Saved\SaveGames\0\<your_save_here>\` 文件夹下多出一个新的 `<GUID>.sav` 存档，这个存档就是你的存档。

4. 关闭服务器，然后将整个专用服务器存档 `PalServer\Pal\Saved\SaveGames\0\<your_save_here>` （必须是带有合作主机新角色的存档！）复制到临时文件夹中，并记住临时文件夹的路径，因为运行脚本需要它。

5. **备份你的存档！**（除非你想和帕鲁永别）

6. 使用 `fix-host-save.py` 脚本将你的旧存档 `00000000000000000000000000000001.sav` 替换成 `<New_GUID>.sav`。

7. 将存档从临时文件夹复制回专用服务器。

8. 启动服务器,你应该能正常进入游戏了。到此，你的存档已经成功迁移。

9. 如果你的伙伴们不再为你攻击或在基地里工作，请按照[帕鲁错误](#帕鲁错误)解决方法修复它们。


## 将存档从合作模式迁移到另一个合作模式/从主机迁移到合作模式

准备工作
- 服务器的管理员权限
- Python>3.8
- 下载此群文件的存档修复工具里的PalRepairKit.zip，解压到合适地点
- 关闭服务器，备份服务器游戏存档
- 开启服务器

正文
### 第一步：获取PID
使用自己合适的方法获取PID，以下讲一个比较简单的方法。
1. 使用盗版进入游戏，输入在聊天框里输入服务器的管理员密码(在设置里的名字是adminpassword=<密码>，不是服务器进入的密码)，认证为管理员。
/adminpassword <密码>
2. esc打开游戏菜单，找到自己的人物名字后面的一串数字，记下。
3. 打开windows的计算器（win7开始就有这个功能了），切换为程序员模式，输入这串数字，查看HEX后16进制数。
![image](https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/cf360104-f1a5-4c85-a593-6cd186871d34)
![image](https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/59cfaeea-4ba4-41ce-910d-355ab3550d5a)


5. 在savegames/0/<英文数字组合>/players/文件夹下找到与这串16进制数相同存档.sav文件，这个存档为你的原始存档。
### 第二步 新建存档
1. 登录正版steam账号，使用正版账号新建角色，进入游戏开启一个传送点。
2. 使用第一步的操作，记录你正版账号新建的角色，此为你的新建存档。
3. 退出游戏，关闭服务器。

### 第三部 存档转移
- 使用PalRepairKit里的fix-host-save.py文件（用法）将老存档的内容合并到新建存档。
- 具体步骤参考转移合作模式存档到服务器。
- 具体bug解决方式参考已知bug。


**如果你成功了，欢迎你也写教程发出来。社区因你而精彩。**

## 已知bug

### 在PART II重建玩家存档之后仍需要新建角色

请你新建角色，关闭服务器。
之后仅将players文件夹覆盖。
这一次不需要转移leve.sav文件。

### 帕鲁错误

玩家拥有的帕鲁不会在基地做任何事情，或者被举起。这可能是由于帕鲁没有正确被识别为你的帕鲁。

解决方法：在新服务器上，在保存修复后，抛弃帕鲁并重新捕获帕鲁。

如果你还有不懂的地方，可以加入QQ群咨询我，我是群主

<img src="https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/1296a517-9958-44ea-be73-a2433d455544" width="200">
<img src="https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/7016e6c9-73a8-41b1-9e7c-671372d78669" width="200">
