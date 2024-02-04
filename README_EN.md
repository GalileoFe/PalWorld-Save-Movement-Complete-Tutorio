# PalWorld-Save-Movement-Complete-Tutorial

> PalWorld-Save-Movement-Complete-Tutorial
> 
> 
> Anyone is welcome to translate this tutorial into other languages.
> 

# Complete Guide to Transferring Pet Paradise Save Files

> :warning:
> 
> 
> This transfer operation may cause the following issues with your saved files:
> 
> - Being taken away by the Dark Witch's Cat.
> - Being exploded by the Bomb Bird.
> 
> I still strongly recommend making thorough backups before performing any operations. It's better to be safe than sorry. Stay optimistic and calm while preparing for the worst. Follow me step by step to complete this task.
> 

## Introduction

This guide is intended for players who have an adventurous spirit, some computer technical experience, and most importantly - patience. I will guide you through the process of transferring your Pet Paradise save files.

## Preparation

Before we begin, please make sure you have the following prepared:

1. Archive of the old host - You need to obtain the saved file of the creature Palu from your old host. This is an essential part of the transfer process.
2. New cloud server - Prepare a new cloud server to store and run the new save file of Palu.
3. Save file location - Find the path `Pal\\Saved\\SaveGames\\<random_numbers>` in your server folder and save it. I recommend packing the entire "Saved" folder for future operations.
4. Download the archive - I will provide a packaged archive that you can download from [here](https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/releases/tag/RepairKit). It contains all the necessary files for the save file transfer.
5. Extract to a suitable location - Extract the archive to a suitable location. For example, you can create a folder named "mirage_save" to store the extracted files.
6. Confirm the server for your existing saved file
    - LinuxServer Manual Install with Official Guide
    - LinuxServer service panel server
    - WinServer with steamcmd
    - WinServer with steamclient
    - Windows cooperative mode

Make sure you have completed the above steps, and then we can proceed to the next part of the tutorial.

## Determine the source of your saved player PID

The player PID in PalWorld is determined based on two factors (based on my unverified experience):

1. The player's steamID, which is the ID in their profile.
2. **The APPID of the server** (important)
    
    > The APPID can be found in the server's output, which will display SteamAPPID = <NUMBER>.
    > 
    > - For Windows users, you have three types of APPIDs:
    >     - No ID, which occurs when the Steam library is not loaded.
    >     - ID = 1623730, which is the standalone client installed through steamcmd.
    >     - ID = 2394010, which is the standalone client installed through steamclient or the cooperative mode.
    > - For Linux users, you have two types of APPIDs:
    >     - No ID, which occurs when [steamclient.so](http://steamclient.so/) is not loaded.
    >     - ID = 2394010, which is the ID when following the official installation tutorial.

## Server APPID types

- No ID
- 1623730 = PalWorld Game
- 2394010 = PalWorld Standalone Server
    
    > :warning: Reports indicate that 1623730 and 2394010 have the same effect and can be considered equivalent.
    > 

## Server Transfer

1. Make sure the APPID of your server remains the same before and after the transfer. (16 is equivalent to 23)
2. Log in to the server to create a new world.
3. **Shut down the server.**
4. Delete `PalServer\\Pal\\Saved\\SaveGames\\0\\`
5. For Linux:
In the `PalServer\\Pal\\Saved\\Config\\LinuxServer\\GameUserSettings.ini` file, change `DedicatedServerName` to match the name of the saved folder. For example, if the saved folder name is `2E85FD38BAA792EB1D4C09386F3A3CDA`, change `DedicatedServerName` to `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA`.
For Windows:
In the `PalServer\\Pal\\Saved\\Config\\WindowsServer\\GameUserSettings.ini` file, change `DedicatedServerName` to match the name of the saved folder. For example, if the saved folder name is `2E85FD38BAA792EB1D4C09386F3A3CDA`, change `DedicatedServerName` to `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA`.
6. Copy your saved game to `PalServer\\Pal\\Saved\\SaveGames\\0\\`.
    
    > Similar to PalServer\\Pal\\Saved\\SaveGames\\0\\<your_save_here>\\
    > 
7. Delete `PalServer\\Pal\\Saved\\SaveGames\\0\\<your_save_here>\\WorldOption.sav` (**This may not exist, which is normal. If it doesn't exist, there's no need to delete it**) to allow modifications to `PalWorldSettings.ini`. (This will cause players to lose their map and respawn points)
8. Log in to the server and verify if the transfer was successful. If it wasn't, go back to determine the source of your saved game player PID.

Your save game should have been transferred successfully.

## Migrating from Cooperative Mode to Server

The biggest difference between Cooperative Mode and Server is the migration of host saves. In Cooperative Mode, the ID of the host player in the local save file is `00000000000000000000000000000001.sav`.

Therefore, Paru Discord has a genius who wrote a Python script to convert the saved file. The script can be found at the following address:

[Palworld Host Save Fix](https://github.com/xNul/palworld-host-save-fix)

Here are the steps:

### Before starting

1. Download the Python script from GitHub, [palworld-host-save-fix](https://github.com/xNul/palworld-host-save-fix), which is also available in the files I provided.
2. Install Python > 3.10
3. Obtain [uesave-rs](https://github.com/trumank/uesave-rs), which is also available in the files I provided, named uesave.exe.

### Explanation of the Python script

> :cactus: GUID = Hexadecimal version of PID, and the file name of the save file is GUID
> 

Command:

```bash
python fix-host-save.py <uesave.exe> <save_path> <new_guid> <old_guid>
```

> <uesave.exe> - Path to uesave.exe
> 
> 
> `<save_path>` - Path to the save folder
> 
> `<new_guid>` - GUID of the player on the new server
> 
> `<old_guid>` - GUID of the player on the old server
> 

Example:

```bash
python fix-host-save.py "C:\\Users\\John\\.cargo\\bin\\uesave.exe" "C:\\Users\\John\\Desktop\\my_temporary_folder\\2E85FD38BAA792EB1D4C09386F3A3CDA" 6E80B1A6000000000000000000000000 00000000000000000000000000000001
```

> This script is used to migrate a GUID.sav to another GUID.sav while modifying Level.sav to ensure data consistency.
> 

> ⚠️⚠️⚠️ <save_path> is the entire folder that includes Level.sav, including the Players file. ⚠️⚠️⚠️
The document tree is as follows:
> 

```bash
PalRepairkit/
│
├── uesave.exe
├── fix-host-save.py
└── 2E85FD38BAA792EB1D4C09386F3A3CD/
    │
    ├── Level.sav
    ├── Levelmeta.sav
    └── players/
        │
        ├── 6E80B1A6000000000000000000000000.sav
        └── 809D6A91000000000000000000000000.sav
```

### Start

### PART I:

1. Determine your server APPID before and after the transfer remains the same.
2. Log in to the server to create a new world.
3. **Shut down the server.**
4. Delete `PalServer\\Pal\\Saved\\SaveGames\\0\\`
5. For Linux:
In the `PalServer\\Pal\\Saved\\Config\\LinuxServer\\GameUserSettings.ini` file, change `DedicatedServerName` to match the name of the saved folder. For example, if the saved folder name is `2E85FD38BAA792EB1D4C09386F3A3CDA`, then change `DedicatedServerName` to `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA`. For Windows:
In the `PalServer\\Pal\\Saved\\Config\\WindowsServer\\GameUserSettings.ini` file, change `DedicatedServerName` to match the name of the saved folder. For example, if the saved folder name is `2E85FD38BAA792EB1D4C09386F3A3CDA`, then change `DedicatedServerName` to `DedicatedServerName=2E85FD38BAA792EB1D4C09386F3A3CDA`.
6. Copy your save files to `PalServer\\Pal\\Saved\\SaveGames\\0\\`.
    
    > Similar to PalServer\\Pal\\Saved\\SaveGames\\0\\<your_save_here>\\
    > 
7. Delete `PalServer\\Pal\\Saved\\SaveGames\\0\\<your_save_here>\\WorldOption.sav` (**It may not exist, which is normal and does not need to be deleted**) to allow modifications to `PalWorldSettings.ini`. (This will cause players to lose maps and respawn points)
8. **Ask your friend to log in to the server to verify if the transfer was successful. If it is not successful, go back to determine the source of your save player PID.**

### PART II

1. If successful, now start resolving your save issues as the host.
2. Log in to the server, create a character, and create a save point.
3. At this point, you will see a new `<GUID>.sav` save file in the `PalServer\\Pal\\Saved\\SaveGames\\0\\<your_save_here>\\` folder. This is your saved file.
4. Shut down the server, then copy the entire dedicated server save `PalServer\\Pal\\Saved\\SaveGames\\0\\<your_save_here>` (with the new cooperative host character!) to a temporary folder and remember the path to the temporary folder as it will be needed to run the script.
5. **Backup your save file!** (Unless you want to say goodbye to Palu forever)
6. Use the `fix-host-save.py` script to replace your old save file `00000000000000000000000000000001.sav` with `<New_GUID>.sav`.
7. Copy the saved file back to the dedicated server from the temporary folder.
8. Start the server, and you should be able to enter the game normally. At this point, your saved file has been successfully transferred.
9. If your companions are no longer attacking or working in the base, follow the instructions in Palu Errors to fix them.

## Transferring Save Files from Cooperative Mode to Another Cooperative Mode/From Hosting to Cooperative Mode

Preparation:

- Administrator access to the server
- Python >3.8
- Download the archive repair tool PalRepairKit.zip from the files of this group, extract it to a suitable location
- Close the server and backup the game save file
- Start the server

Main Content:

### Step 1: Get the PID

Use a suitable method to get the PID. Here, we will explain a relatively simple method.

1. Use a pirated version to enter the game and enter the server's administrator password in the chat box (the name in the settings is adminpassword=<password>, not the password used to enter the server) to authenticate as an administrator.
/adminpassword <password>
2. Press "esc" to open the game menu and find the string of numbers behind your character's name. Take note of it.
3. Open the calculator on Windows (available since Windows 7), switch to programmer mode, enter this string of numbers, and view the hexadecimal (HEX) value.
![image](https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/cf360104-f1a5-4c85-a593-6cd186871d34)
![image](https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/59cfaeea-4ba4-41ce-910d-355ab3550d5a)
    
4. In the savegames/0/<combination of English numerals>/players/ folder, find the .sav file with the same hexadecimal value. This file is your original save file.

### Step 2: Create a New Save File

1. Log in to your legitimate Steam account and use it to create a character. Enter the game and open a teleportation point.
2. Use the steps from the first step to record the character created with your legitimate account. This will be your new save file.
3. Exit the game and close the server.

### Step 3: Save File Transfer

- Use the [fix-host-save.py](http://fix-host-save.py/) file in PalRepairKit (usage) to merge the contents of the old save file into the newly created save file.
- For specific steps, refer to [Transfer Cooperative Mode Save File to Server](https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/blob/main/README.md#%E4%BB%8E%E5%90%88%E4%BD%9C%E6%A8%A1%E5%BC%8F%E8%BF%81%E7%A7%BB%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A8).
- For specific bug solutions, refer to [Known Bugs](https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/blob/main/README.md#%E5%B7%B2%E7%9F%A5bug).

**If you succeed, feel free to write a tutorial and share it. The community thrives because of you.**

## Known Bugs

### After rebuilding player save data in PART II, a new character is still required

Please create a new character and then close the server.
Afterwards, only overwrite the players folder.
This time, there is no need to transfer the leve.sav file.

### Palu Error

The Palu owned by the player does not do anything in the base or get lifted up. This may be due to the Palu not being properly recognized as yours.

Solution: On the new server, after saving the fix, discard the Palu on the ground and then pick it up again.

### Rebuilding Game Character

> ⚠⚠⚠ This fix is only for cases where a new character is required when entering the save file ⚠⚠⚠
> 

> For Windows Server users:
> 
> 1. If you don't have Steam installed on your system:
> - Please install Steam.
> 1. If you already have Steam installed on your system:
> - Please uninstall the existing Steam and then reinstall it.

> For Linux users:
> 
> - Delete the `~/.steam/sdk64` folder to address the issue of rebuilding the game character.
> - Docker installation: Create an empty folder mapping `/home/steam/.steam/sdk64` as read-only.
> If it still doesn't work, run `docker exec -it <container name> bash`, [enter the container and search for steamclient.so](http://steamclient.so/), the command is `find / -name [steamclient.so](http://steamclient.so/)`, and map all of them to empty read-only files.

### Server Save File Crashes After Opening

The server save file has been successfully migrated, but the server crashes after entering the game for a while:

1. Please have the administrator check the current permission settings of the server save file folder.
2. If it is confirmed that the folder is set as read-only, please change the permission of the save file folder to 777 (allowing read, write, and execute operations).
3. On a Linux system, you can use the following command to change permissions:
    
    ```bash
    chmod 777 [save file folder path]
    ```
    

> Please make sure to replace [save file folder path] with the actual folder path.
Note:
> 
- Setting the permission to 777 will allow all users to read, write, and execute operations on the folder. Please make sure this operation meets your security and privacy requirements.

If you still have any questions, you can join the QQ group and consult me. I am the group owner.

<img src="https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/1296a517-9958-44ea-be73-a2433d455544" width="200">
<img src="https://github.com/GalileoFe/PalWorld-Save-Movement-Complete-Tutorio/assets/138156577/7016e6c9-73a8-41b1-9e7c-671372d78669" width="200">

# Acknowledgements

https://github.com/xNul/palworld-host-save-fixhttps://github.com/burpheart/Palworld-Reverse-Note
