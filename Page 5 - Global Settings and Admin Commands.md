# 5. Global Settings and Admin Commands

This section covers the main `BS_KeyRoom_Settings.json` file and the in-game commands available to administrators.

## 5.1. Global Settings (BS_KeyRoom_Settings.json)

This file controls the global settings for the mod and is the central place to define loot pools that can be used by any door.

**File Location:** `$profile/BS_KeyRoom/BS_KeyRoom_Settings.json`

### Detailed Example

Below is a more complete and detailed example demonstrating how to structure your lootPools for different scenarios. The JSON code is properly formatted for readability.

```json
{
    "debug_build": 0,
    "admin_log": 1,
    "showDoorTimerText": 1,
    "lootPools": [
        {
            "lootPoolName": "Global_Military_Weapons_T4",
            "rewards": [
                {
                    "name": "SVD",
                    "chanceToSpawn": 0.40,
                    "quantityMin": 1,
                    "quantityMax": 1,
                    "attachments": [
                        { 
                            "name": "PSO1Optic", 
                            "quantity": 1 
                        },
                        { 
                            "name": "Mag_SVD_10Rnd", 
                            "quantity": 10 
                        }
                    ]
                },
                {
                    "name": "FAL",
                    "chanceToSpawn": 0.60,
                    "quantityMin": 1,
                    "quantityMax": 1,
                    "attachments": [
                        { 
                            "name": "Fal_OeBttstck", 
                            "quantity": 1 
                        },
                        { 
                            "name": "ACOGOptic", 
                            "quantity": 1 
                        },
                        { 
                            "name": "Mag_FAL_20Rnd", 
                            "quantity": 20 
                        }
                    ]
                }
            ]
        },
        {
            "lootPoolName": "Global_Medical_Supplies",
            "rewards": [
                {
                    "name": "BandageDressing",
                    "chanceToSpawn": 1.0,
                    "quantityMin": 4,
                    "quantityMax": 8,
                    "attachments": []
                },
                {
                    "name": "Morphine",
                    "chanceToSpawn": 0.8,
                    "quantityMin": 2,
                    "quantityMax": 4,
                    "attachments": []
                },
                {
                    "name": "SalineBagIV",
                    "chanceToSpawn": 0.5,
                    "quantityMin": 1,
                    "quantityMax": 1,
                    "attachments": []
                }
            ]
        },
        {
            "lootPoolName": "Global_Industrial_Tools",
            "rewards": [
                {
                    "name": "SledgeHammer",
                    "chanceToSpawn": 0.2,
                    "quantityMin": 1,
                    "quantityMax": 1,
                    "attachments": []
                },
                {
                    "name": "Pliers",
                    "chanceToSpawn": 0.8,
                    "quantityMin": 1,
                    "quantityMax": 1,
                    "attachments": []
                },
                {
                    "name": "WeaponCleaningKit",
                    "chanceToSpawn": 1.0,
                    "quantityMin": 1,
                    "quantityMax": 1,
                    "attachments": []
                }
            ]
        }
    ]
}
```
Parameter Explanations
- debug_build: (0 or 1) Enables debug mode.

1: Enables the BS_DoorLocker tool for creating new door configs in-game.

0: Disables debug mode. Set this to 0 for your live server!

- admin_log: (0 or 1) If 1, detailed logs about player actions (opening doors, using keycards) will be generated in the $profile/BS_KeyRoom/logs/ folder. This is useful for tracking activity.

- showDoorTimerText: (0 or 1) If 1, players will see a contextual action text on open doors indicating how much time is left before they close (e.g., "Door closing in 4:32").

- lootPools: (Array of Objects) This is where you can define all the global loot pools you want to use across your various door configurations. Any pool defined here can be referenced by its lootPoolName in any door's JSON file.

How it Works: Defining loot pools here allows you to reuse them easily. In the example above, you could have a military bunker use the "Global_Military_Weapons_T4" pool, while a hospital room could use the "Global_Medical_Supplies" pool. This keeps your configurations clean and easy to manage.

For a complete guide on the structure of rewards and attachments, please see the [[3. Advanced Loot System]] page.

- 5.2. Admin Management
Adding Admins
To use admin commands, you must first add administrators to the mod.

Open the BS_KeyRoom/admins.txt file.

Add the Steam64ID of each administrator, with one ID per line.

- In-Game Commands
Admins can use the following command in the in-game chat:

!kcreload

- This command will reload all BS KeyRoom configuration files from the profile folder (DoorConfigs, Settings, and ItemNames) and apply them instantly without requiring a server restart. This is extremely useful for testing and making live adjustments.
