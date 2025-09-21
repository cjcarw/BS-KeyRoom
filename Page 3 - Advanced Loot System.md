# 3. Advanced Loot System

The loot system is the most powerful feature of BS KeyRoom. You can configure it inside a door's JSON file through the `containers` array and the `doorSpecificLootPools` array.

## 3.1. Loot Pools: The Foundation

A "Loot Pool" is a list of potential items that can spawn. You can define them in two places:

- **Global Pools**: Defined in `BS_KeyRoom_Settings.json`. These pools can be used by any door on the server.
- **Door-Specific Pools**: Defined inside a door's JSON file in the `doorSpecificLootPools` array. These pools can only be used by the containers within that same door configuration.

### How Rewards are Structured (Core Example)

Let's break down an advanced item configuration. This structure can be used inside the `rewards` array of a loot pool, or inside the `fixedItems` array of a container.

```json
{
    "name": "SNAFUKivaari_Tan_GUN",
    "quantity": 1,
    "attachments": [
        {
            "name": "SNAFUKivaari_10rdMag",
            "quantity": 10,
            "random_names": [],
            "attachments": []
        },
        {
            "name": "",
            "quantity": 1,
            "random_names": [
                "ACOGOptic",
                "M68Optic",
                "BUISOptic"
            ],
            "attachments": [
                {
                    "name": "Battery9V",
                    "quantity": 1,
                    "random_names": [],
                    "attachments": []
                }
            ]
        }
    ]
}
```
Analysis of the Example:
- The Base Item: "name": "SNAFUKivaari_Tan_GUN"

This is the main item that will be spawned.

- Direct Attachment: "name": "SNAFUKivaari_10rdMag"

This is a simple attachment. The Kivaari will always spawn with this specific magazine attached. The magazine itself will spawn with 10 rounds because "quantity": 10.

- Randomized Attachment: "random_names": [ "ACOGOptic", "M68Optic", "BUISOptic" ]

This is a key feature. The name field is left empty (""), and the random_names array is used instead.

The mod will randomly select one of the three optics from the list and attach it to the weapon. This is perfect for creating variety.

- Nested Attachment: attachments: [ { "name": "Battery9V", ... } ]

This attachment is inside the randomized optic attachment.

This means that whichever optic is randomly chosen, it will spawn with a Battery9V inside it. You can nest attachments as deep as you need.

- 3.2. Container Configuration Types
Now, let's see how to use this loot structure within the different types of containers you can define in your door's main JSON file.

- A. Fixed Loot (useFixedLoot and fixedItems)
This method is for loot that you want to always spawn in a container. It's predictable.

- useFixedLoot: Must be set to 1 to enable this feature for the container.

- fixedItems: An array of items to spawn, using the structure we analyzed above.

- quantityMinPercent / quantityMaxPercent: Optional parameters for items. For example, you can make a magazine spawn with a random amount of ammo between 50% and 100% of its capacity.
Example:
```
json
{
    "referenceName": "GuaranteedLootCrate",
    "className": "BS_Box1_White",
    "useFixedLoot": 1,
    "fixedItems": [
        {
            "name": "Mag_STANAG_30Rnd",
            "quantity": 30,
            "quantityMinPercent": 0.5,
            "quantityMaxPercent": 1.0
        },
        {
            "name": "SNAFUKivaari_Tan_GUN",
            "quantity": 1,
            "attachments": [
                {
                    "name": "SNAFUKivaari_10rdMag",
                    "quantity": 10
                }
            ]
        }
    ]
}
```

B. Randomized Loot from Pools
This method spawns a random number of items from one or more pre-defined loot pools, creating dynamic and unpredictable rewards.

- lootPoolName: Use this if you want to pull loot from a single pool.

- randomLootPools: An array of loot pool names. If spawnFromAllPools is 0, one pool will be chosen randomly from this list.

- spawnFromAllPools: If set to 1, the system will attempt to spawn items from every pool listed in randomLootPools.

- lootMin / lootMax: The total number of items to spawn from the selected pool(s).

- preventDuplicateLoot: If 1, the system will not spawn the same item type more than once in this container.
Example:
```
json
{
    "referenceName": "RandomMilitaryCrate",
    "className": "BS_Box4_Green",
    "randomLootPools": [
        "Global_Military_Weapons_T4",
        "Global_Military_Gear_T4"
    ],
    "spawnFromAllPools": 1,
    "lootMin": 1,
    "lootMax": 2
}
```
- C. Integration with LBmaster Rework
- If you use the LBmaster_Rework mod, you can make a container spawn a full preset from that mod, ignoring all other loot settings like fixedItems and lootPoolName.

- lb_preset_name: (String) The exact name of the preset from LBmaster_Rework's configuration that you want to spawn.

Example:
```
json
{
    "referenceName": "LBmasterPresetCrate",
    "className": "BS_Guncase_Black",
    "lb_preset_name": "Full_SNAFU_M4_Kit"
}
```
- D. Replacement Containers

Allows a common container to sometimes be replaced by a rarer one, with its own loot rules.

Parameters:

- replacementChance: Probability (0.0 → 1.0).

- replacementClassName: New container class.

- replacementLootPoolName: Overrides loot pool.

- replacementRandomLootPools: Overrides random pools.

- replacementLootMin / replacementLootMax: Overrides loot counts.

- replacementUseFixedLoot: Enables fixed loot in replacement.

- replacementFixedItems: Items that spawn only if replaced.

- replacementPreventDuplicateLoot: Duplicate prevention for replacement.

- replacement_lb_preset_name: LBmaster preset for replacement.

 Example 1: Standard Replacement (No LBmaster)
```
{
    "referenceName": "MedicalCrate_Or_RareWeapon",
    "className": "BS_Box1_White",
    "lootPoolName": "Global_Medical_Supplies",
    "lootMin": 2,
    "lootMax": 4,
    "replacementChance": 0.15,
    "replacementClassName": "BS_Guncase_Black",
    "replacementUseFixedLoot": 1,
    "replacementFixedItems": [
        {
            "name": "SNAFUKivaari_Tan_GUN",
            "quantity": 1,
            "attachments": [
                {
                    "name": "SNAFUKivaari_10rdMag",
                    "quantity": 10
                },
                {
                    "name": "",
                    "random_names": [
                        "ACOGOptic",
                        "M68Optic"
                    ]
                }
            ]
        }
    ],
    "replacementLootPoolName": "",
    "replacementLootMin": 0,
    "replacementLootMax": 0
}
```

How it works:

- 85% → White medical box, spawns 2–4 items from Global_Medical_Supplies.

- 15% → Black guncase, spawns one Kivaari with mag + random optic.

- Example 2: Replacement with LBmaster Preset
```
{
    "referenceName": "NormalCrate_Or_LBmaster_Kit",
    "className": "BS_Box4_Black",
    "lootPoolName": "Global_Industrial_Tools",
    "lootMin": 2,
    "lootMax": 3,
    "replacementChance": 0.10,
    "replacementClassName": "BS_Guncase_Black",
    "replacement_lb_preset_name": "Full_SNAFU_SVD_Kit"
}

```
How it works:

- 90% → Spawns 2–3 industrial tools.

- 10% → Spawns a black guncase with a full SVD kit preset.
