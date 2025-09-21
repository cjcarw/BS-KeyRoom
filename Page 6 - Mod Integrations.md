# 6. Mod Integrations

BS KeyRoom is designed to work well with other popular mods, enhancing its functionality.

## Expansion Mod

If the DayZ Expansion mod bundle is detected on your server, BS KeyRoom will automatically integrate with some of its features:

- **Advanced Notifications**: When `use_announcement` is enabled for a door, the mod will use the Expansion notification system instead of the default one. This allows for more visually appealing announcements with custom colors. You can configure the color using the `announcement_color_rgba` parameter in the door's JSON file.

## CFTools / GameLabs

BS KeyRoom has built-in support for logging important server events to CFTools or GameLabs if they are running on your server. This provides server owners with a powerful audit trail.

- **Logged Actions**: The mod will log an event whenever a player successfully opens a keycard door. The log includes:
  - The player's name and ID.
  - The keycard they used.
  - The `Location_Name` of the door they opened.
  
This helps you track who is accessing high-tier loot zones and when.

## Bastardos Hacked Crate (BSHC)

You can configure a hackable crate from the BSHC mod to spawn as part of the door event.

- **Configuration**: In the door's JSON file, set `spawn_hacked_crate` to `1` and complete the following parameters:
  - `hacked_crate_classname`: The classname of the crate to spawn.
  - `hacked_crate_position`: The vector where the crate will appear.
  - `hacked_crate_orientation`: The orientation of the spawned crate.
  - `hacked_crate_config_id`: The unique ID from the BSHC config that defines the crate's hacking time and loot.

## LBmaster_Rework

BS KeyRoom is compatible with spawning loot presets from the LBmaster_Rework mod.

- **Configuration**: Instead of defining a `lootPoolName` or `fixedItems` for a container, you can specify an `lb_preset_name`. The mod will then call the LBmaster functions to spawn the entire preset inside the container. This is a quick way to integrate complex loot setups.
