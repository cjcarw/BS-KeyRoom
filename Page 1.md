# 1. Installation and Setup

This page covers the initial setup and file structure of the BS KeyRoom mod.

## Workshop Installation

1. Subscribe to the mod on the Steam Workshop.
2. Add the mod to your server's `-mod` launch parameter (`-mod=@BS_KeyRoom`).
3. Copy the `.bikey` file from the mod's `keys` folder to your server's `keys` folder.

## Configuration File Structure

Once the mod is loaded for the first time on your server, it will create the following folder and file structure in your profile directory (`$profile`):
$profile/
└── BS_KeyRoom/
├── logs/ // Directory for the mod's log files.
├── DoorConfigs/ // This is where the JSON for each door goes!
│ └── GreenMountainRedKeycard.json (Example)
├── admins.txt // A list of Steam64IDs for server admins.
├── BS_KeyRoom_Settings.json // Global settings and global loot pools.
├── BS_KeyRoom_ItemNames.json // Names, descriptions, and uses for keys/keycards.
└── BS_KeyRoom_Cooldowns.json // (Internal Use) Saves the state of door cooldowns.

- **DoorConfigs/**: This is the most important folder. Each `.json` file inside represents one configured door or door group on the map.
- **BS_KeyRoom_Settings.json**: This file controls the mod's global behavior.
- **BS_KeyRoom_ItemNames.json**: This file allows you to customize your keys and keycards.
- **admins.txt**: A simple text file where you list the Steam64IDs of players who can use admin commands.

With the files generated, you are now ready to start configuring your doors.

**Next Step:** [[2. Door Configuration]]
