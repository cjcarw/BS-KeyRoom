# 2. Door Configuration (JSON)

Every door you want the mod to control must have its own `.json` configuration file inside the `BS_KeyRoom/DoorConfigs/` folder.

## 2.1. Auto-Creating Configs with the Admin Tool

To make creating new door configurations incredibly easy, the mod includes an in-game admin tool.

**Steps:**

1. **Enable Debug Mode**: In your `BS_KeyRoom_Settings.json` file, make sure `debug_build` is set to `1` (or `true`).
2. **Get The Tool**: As an admin, spawn the item `BS_DoorLocker`.
3. **Aim and Generate**: With the `BS_DoorLocker` in your hands, aim at the door you wish to configure and hold down the left mouse button. The action is called "Setup Keycard Door".
4. **Check Your Files**: Upon completion, a new `.json` file will be generated in your `DoorConfigs` folder. This file will contain the building coordinates, door position, and door index, ready for you to customize.

## 2.2. Detailed Door JSON Parameters

Below is a comprehensive list of every parameter you can use in a door's JSON file.

```json
{
    "x": 3689.39, "y": 5985.54, "z": 403.74,
    "building_x": 3686.41, "building_y": 5982.14, "building_z": 407.67,
    "door_indices": [ 0, 1 ],
    "Location_Name": "GreenMountain_Barracks_Main",
    "BuildingClassName": "Land_Mil_Barracks5",
    "keycard_class_name": "BS_keycard_lab_red",
    "unlockOnly": 0,
    "use_announcement": 1,
    "announcement_title": "ALERT",
    "announcement_text": "A red keycard has been activated at Green Mountain.",
    "announcement_color_rgba": "255,220,53,69",
    "use_alarm": 1,
    "alarm_sound": "Alarm_Military",
    "alarm_duration": 45,
    "alarm_loop_delay": 1.8,
    "min_unlock_time": 5,
    "max_unlock_time": 10,
    "min_restock_time": 300,
    "max_restock_time": 600,
    "containers_only": 0,
    "min_containers_to_spawn": 1,
    "max_containers_to_spawn": 2,
    "persistCooldownOnRestart": 1,
    "use_safety_teleport": 1,
    "safety_teleport_radius": 50.0,
    "use_custom_teleport_points": 1,
    "custom_teleport_points": [ "3670.0 402.0 5995.0" ],
    "containers": [],
    "doorSpecificLootPools": [],
    "spawn_hacked_crate": 0,
    "hacked_crate_classname": "",
    "hacked_crate_position": "0 0 0",
    "hacked_crate_orientation": "0 0 0",
    "hacked_crate_config_id": ""
}
```
Parameter Explanations
Core Identification
x, y, z: Coordinates of the door. Do not modify manually; use the admin tool.

building_x, building_y, building_z: Coordinates of the building. Do not modify manually.

door_indices: (Array of Integers) A list of all door indexes in the building that will be opened by this configuration. A single keycard can open multiple doors at once.

Location_Name: (String) A unique name to identify this door in logs. Must be unique across all your door files.

BuildingClassName: (String) The classname of the building. Retrieved automatically by the admin tool.

keycard_class_name: (String) The classname of the item (key or keycard) required to open this door.

unlockOnly: (0 or 1) If 1, the keycard only unlocks the door but does not physically open it. The player must open it manually. Default is 0.

Announcements & Alarms
use_announcement: (0 or 1) If 1, sends a global message to the server when the keycard is used.

announcement_title: (String) The title of the global announcement.

announcement_text: (String) The body message of the announcement.

announcement_color_rgba: (String) Color of the announcement in "A,R,G,B" format (for Expansion mod).

use_alarm: (0 or 1) If 1, plays a looping alarm sound at the door's location.

alarm_sound: (String) The SoundSet that will be played.

alarm_duration: (Integer) Total duration in seconds the alarm will sound for.

alarm_loop_delay: (Float) Time in seconds between each loop of the alarm sound.

Timers
min_unlock_time / max_unlock_time: (Integers) The random time in seconds it takes for the door to open after the card is swiped.

min_restock_time / max_restock_time: (Integers) The random time in seconds the door remains open before it automatically closes.

Loot & Containers
containers_only: (0 or 1) If 1, loot containers are static and already present on the server. The door will not be openable, serving as a persistent loot zone.

min_containers_to_spawn / max_containers_to_spawn: (Integers) The min/max number of containers that will spawn from the containers list. Set to -1 to spawn all.

See [[3. Advanced Loot System]] for details on containers and doorSpecificLootPools.

Safety & Restarts
persistCooldownOnRestart: (0 or 1) If 1, the door's open state and timer will survive a server restart. Highly recommended.

use_safety_teleport: (0 or 1) If 1, teleports players out of the room before the door closes to prevent them from getting trapped.

safety_teleport_radius: (Float) The radius in meters for the safety teleport check.

use_custom_teleport_points: (0 or 1) If 1, uses one of the points defined in custom_teleport_points for the teleport.


