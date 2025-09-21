# 3. Advanced Loot System

The loot system is defined within the `containers` and `doorSpecificLootPools` parameters in a door's JSON file.

## 3.1. Configuring Loot Pools

A "Loot Pool" is a list of items that can spawn. You can define them in two places:

- **Global Pools**: In `BS_KeyRoom_Settings.json`. These can be used by any door.
- **Door-Specific Pools**: In the `doorSpecificLootPools` parameter of a door's JSON. These can only be used by that specific door.

**Example of a Loot Pool:**

```json
{
    "lootPoolName": "Weapons_Tier4",
    "rewards": [
        {
            "name": "SVD",
            "chanceToSpawn": 0.50,
            "quantityMin": 1,
            "quantityMax": 1,
            "attachments": [
                {
                    "name": "PSO1Optic",
                    "quantity": 1,
                    "random_names": [],
                    "attachments": []
                },
                {
                    "name": "",
                    "quantity": 1,
                    "random_names": [ "AK_Suppressor", "ImprovisedSuppressor" ],
                    "attachments": []
                }
            ]
        }
    ]
}
```
- lootPoolName: A unique name for this pool.

- rewards: An array of items that can spawn.

- name: The className of the item.

- chanceToSpawn: The weighted probability of this item being chosen.

- quantityMin / quantityMax: The random quantity of the item that will spawn.

- attachments: An array to add attachments. You can nest attachments inside other attachments.

- random_names: (Array of Strings) If the name field is empty, you can use this array to have the system pick one attachment randomly from the list.
- 3.2. Container Configuration
Inside the door's JSON, the containers array lists all possible containers that can spawn.

Example of a Container:

```
{
    "referenceName": "Weapon_Crate_1",
    "className": "BS_Guncase",
    "position": [ 3678.13, 407.20, 5993.55 ],
    "orientation": [ -123.19, 0.0, 0.0 ],
    "spawnChance": 1.0,
    "lootPoolName": "Weapons_Tier4",
    "lootMin": 1,
    "lootMax": 2,
    "useFixedLoot": 0,
    "fixedItems": [],
    "preventDuplicateLoot": 1
}
```
- referenceName: A unique friendly name for this spawn point.

- className: The classname of the container to spawn.

- position & orientation: The spawn coordinates for the container.

- spawnChance: The weighted chance for this container to be chosen if min/max_containers_to_spawn is used.

- 3.3. Fixed vs. Randomized Loot
- Fixed Loot: To make an item always spawn, set useFixedLoot to 1 and define the items in the fixedItems array. This is great for guaranteed rewards. The structure of a fixedItem is similar to rewards but without chanceToSpawn. You can also use quantityMinPercent and quantityMaxPercent (from 0.0 to 1.0) to define the quantity as a percentage of its max capacity (e.g., for magazines or canteens).

- Randomized Loot: To spawn random items from a pool, set useFixedLoot to 0 and use the following:

lootPoolName: The name of a single pool to draw loot from.

randomLootPools: (Array of Strings) If you provide multiple pool names here, the system will pick one at random to use.

spawnFromAllPools: (0 or 1) If 1, the system will spawn loot from all pools listed in randomLootPools.

lootMin / lootMax: The number of items to spawn from the chosen pool(s).

preventDuplicateLoot: (0 or 1) If 1, prevents spawning the same item classname twice from the same pool in this container.

- 3.4. Replacement Containers
This powerful feature allows a standard container to have a chance of being replaced by a different, often rarer, one with its own unique loot setup.

- replacementChance: (Float) The probability from 0.0 (never) to 1.0 (always) that the replacement will occur.

- replacementClassName: (String) The classname of the container that will spawn if the replacement is successful.

Overriding Loot Configuration: When a replacement occurs, you can completely redefine its loot table using a parallel set of parameters. If these are not defined, the replacement container will be empty.

- replacementLootPoolName: (String) The single loot pool to use for the replacement container.

- replacementRandomLootPools: (Array of Strings) A list of loot pools to randomly choose from for the replacement container.

- replacementLootMin / replacementLootMax: (Integers) Min/Max number of items to spawn from the pool(s) for the replacement.

- replacementUseFixedLoot: (0 or 1) Set to 1 to use fixed loot for the replacement.

- replacementFixedItems: (Array of Objects) A list of fixed items that will always spawn in the replacement container.

- replacementPreventDuplicateLoot: (0 or 1) Prevents duplicate items from spawning in the replacement container.

- replacement_lb_preset_name: (String) If using LBmaster_Rework, this is the preset name for the replacement container.
```        
{
            "referenceName": "Rare_Weapon_Crate",
            "className": "BS_Guncase_Green",
            "position": [
                3678.13,
                407.2,
                5993.55
            ],
            "orientation": [
                -123.0,
                0.0,
                0.0
            ],
            "spawnChance": 0.1,
            "lootPoolName": "Weapons_Rare",
            "lootMin": 1,
            "lootMax": 1,
            "useFixedLoot": 0,
            "fixedItems": [],
            "preventDuplicateLoot": 1,
            "replacementChance": 0.5,
            "replacementClassName": "BS_Guncase_Black",
            "replacementLootPoolName": "Weapons_Super_Rare",
            "replacementLootMin": 1,
            "replacementLootMax": 1,
            "replacementUseFixedLoot": 0,
            "replacementFixedItems": [],
            "replacementPreventDuplicateLoot": 1
}
```
