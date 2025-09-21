# 4. Keys and Keycards Configuration

The `BS_KeyRoom_ItemNames.json` file allows you to customize your keys and keycards without needing to repack PBOs. You can change their in-game names, descriptions, and define their number of uses.

## File Location

You can find this file in your server's profile folder:
`$profile/BS_KeyRoom/BS_KeyRoom_ItemNames.json`

## Structure and Parameters

The file contains a single JSON array called `KeyCardEntries`. Each object in this array represents a key or keycard you want to customize.

**Example:**

```json
{
    "KeyCardEntries": [
        {
            "ClassName": "BS_keycard_lab_red",
            "DisplayAndDescription": "High-Tier Red Keycard|Opens doors to the most dangerous and rewarding zones.",
            "MaxUses": 1
        },
        {
            "ClassName": "BS_Admin_Key",
            "DisplayAndDescription": "Admin Master Key|A key with infinite uses.",
            "MaxUses": -1
        },
        {
            "ClassName": "BS_bluekey1",
            "DisplayAndDescription": "Tisy Prison Key|Access to the prison block at Tisy Military Base.",
            "MaxUses": 5
        }
    ]
}
```
Parameter Explanations
- ClassName: (String) The exact classname of the item you want to modify.

- DisplayAndDescription: (String) A single string containing the in-game name and the description, separated by a pipe character |.

The text before the | becomes the item's display name.

The text after the | becomes the item's tooltip description.

- MaxUses: (Integer) The number of uses for the keycard.

1: Single-use. The item will be destroyed after one use.

1: Multiple uses. The item will have a counter (e.g., [4/5]) and will be destroyed after the last use.

-1: Infinite uses. The item can be used forever.

0: The uses counter will be hidden.
