# PlaceAnywhere — Documentation (English)

**Version:** 1.0.0  
**Author:** MasterCraft  
**Minecraft API:** 1.20+  
**Compatibility:** Paper / Spigot

---

PlaceAnywhere is a Bukkit/Paper plugin that allows authorized players to place plants, flowers, decorations, and other "restricted" blocks on any surface, ignoring Minecraft's vanilla placement rules. For example, you can place a flower on a wooden plank, a mushroom under direct light, or coral outside of water.

---

## Commands

All commands have the aliases `/pa` and `/pla` in addition to the full name `/placeanywhere`.

| Command | Description |
|---|---|
| `/pa` | Enable/disable PlaceAnywhere for yourself |
| `/pa toggle` | Equivalent to `/pa` (toggle for yourself) |
| `/pa on` | Enable PlaceAnywhere for yourself |
| `/pa off` | Disable PlaceAnywhere for yourself |
| `/pa <player>` | Enable/disable PlaceAnywhere for another player |
| `/pa toggle <player>` | Same as above |
| `/pa on <player>` | Enable for another player |
| `/pa off <player>` | Disable for another player |
| `/pa info` | Shows info about your status, mode, plugin version, and session statistics |
| `/pa list` | List of all players with PlaceAnywhere currently enabled |
| `/pa reload` | Reloads the configuration without restarting the server |

---

## Permissions

| Permission | Description | Default |
|---|---|---|
| `placeanywhere.use` | Access to the `/pa` command | op |
| `placeanywhere.toggle` | Enable/disable PlaceAnywhere for yourself | op |
| `placeanywhere.toggle.others` | Enable/disable PlaceAnywhere for other players | op |
| `placeanywhere.reload` | Reload the configuration | op |
| `placeanywhere.notify` | Receive admin notifications when a player enables/disables the mode | op |
| `placeanywhere.bypass.permission` | Bypass permission checks (always enabled) | false |
| `placeanywhere.*` | All permissions listed above | op |

> To grant all permissions to a group with LuckPerms: `lp group admin permission set placeanywhere.* true`

---

## Supported Blocks

The plugin handles the following block categories, each individually toggleable in the config:

| Category | Examples |
|---|---|
| `plants` | Short grass, ferns, dead bushes, all saplings |
| `tall-plants` | Tall grass, large fern, sunflower, lilac, rose bush, peony |
| `flowers` | Dandelion, poppy, blue orchid, allium, cornflower, lily, wither rose, etc. |
| `mushrooms` | Brown mushroom, red mushroom |
| `fungi` | Crimson fungus, warped fungus, nether sprouts |
| `nether-plants` | Nether wart, weeping vines, twisting vines |
| `aquatic` | Kelp, seagrass, sea pickle, all types of coral and coral fans |
| `decorations` | Item frames, paintings, ladders, lanterns, chains, bells, pots, lily pad, end rod, lightning rods, levers, tripwire hooks, buttons |
| `torches` | Normal, soul, and redstone torches (including wall variants) |
| `crops` | Wheat, carrots, potatoes, beetroots, melon/pumpkin stems, sugar cane, bamboo, sweet berry bush, cocoa, etc. |
| `vines` | Vines, glow lichen, cave vines, hanging roots, spore blossom, dripleaf |
| `other` | Everything else not included in the previous categories |

### Blacklist (always excluded blocks)

By default, the following materials can never be placed with PlaceAnywhere (regardless of permissions):

- BEDROCK, BARRIER, COMMAND_BLOCK, CHAIN_COMMAND_BLOCK, REPEATING_COMMAND_BLOCK
- END_PORTAL_FRAME, END_PORTAL, NETHER_PORTAL
- STRUCTURE_VOID, STRUCTURE_BLOCK, JIGSAW

You can modify this list in `config.yml`.

---

## Configuration (`config.yml`)

```yaml
# ============================================================
#   PlaceAnywhere - Configuration
#   Author: MasterCraft
#   Version: 1.0.0
# ============================================================

settings:
  # Default mode on first player use
  # TOGGLE = resets at every login
  # PERSISTENT = saved between logins
  default-mode: TOGGLE

  # If true, PlaceAnywhere is enabled by default for all players
  # with the placeanywhere.toggle permission at login
  enabled-by-default: false

  # If true, every placement is logged in the server console
  log-placements: false

  # If true, players with placeanywhere.notify receive chat messages
  # when another player enables/disables the mode
  notify-admins: true

  # If true, shows visual feedback when toggling the mode
  show-toggle-feedback: true
  # Feedback type: ACTIONBAR | TITLE | CHAT | ALL
  feedback-type: ACTIONBAR

  # Sound played on enable/disable
  sound-on:  BLOCK_NOTE_BLOCK_PLING
  sound-off: BLOCK_NOTE_BLOCK_BASS
  sound-enabled: true

  # Visual particle on placement (NONE to disable)
  placement-particle: VILLAGER_HAPPY
  particle-count: 5

placement:
  # Forces block placement even if vanilla removes it
  force-place: true

  # If true, bypasses WorldGuard/GriefPrevention checks
  # (requires those plugins installed)
  bypass-protection-plugins: false

  # Aggressive mode: manually cancels the vanilla event and sets
  # the block directly. More reliable but more invasive.
  aggressive-mode: true

  # List of materials that PlaceAnywhere can NEVER place
  blacklisted-blocks:
    - BEDROCK
    - BARRIER
    - COMMAND_BLOCK
    - CHAIN_COMMAND_BLOCK
    - REPEATING_COMMAND_BLOCK
    - END_PORTAL_FRAME
    - END_PORTAL
    - NETHER_PORTAL
    - STRUCTURE_VOID
    - STRUCTURE_BLOCK
    - JIGSAW

  # Block categories handled by the plugin
  # Set a category to false to completely disable it
  categories:
    plants: true
    tall-plants: true
    flowers: true
    mushrooms: true
    fungi: true
    nether-plants: true
    aquatic: true
    decorations: true
    torches: true
    crops: true
    vines: true
    other: true

messages:
  prefix: "&8[&6PlaceAnywhere&8] &r"
  enabled: "&aPlaceAnywhere &2ENABLED&r. You can place any block anywhere!"
  disabled: "&cPlaceAnywhere &4DISABLED&r. Returning to vanilla rules."
  no-permission: "&cYou do not have permission to use this command."
  player-only: "&cThis command can only be used by a player."
  reload: "&aConfiguration reloaded successfully!"
  player-not-found: "&cPlayer not found: &e{player}"
  toggled-other-on: "&aPlaceAnywhere enabled for &e{player}&a."
  toggled-other-off: "&cPlaceAnywhere disabled for &e{player}&c."
  notify-admin: "&7[PA] &e{player} &7has {action} PlaceAnywhere."
  blacklisted-block: "&cThis block is blacklisted and cannot be placed anywhere."
  info-header: "&8&m----&r &6PlaceAnywhere Info &8&m----"
  info-status: "  &7Status: {status}"
  info-mode: "  &7Mode: &e{mode}"
  info-version: "  &7Version: &e{version}"
  info-author: "  &7Author: &eMasterCraft"
  list-header: "&8&m----&r &6Players with PlaceAnywhere enabled &8&m----"
  list-entry: "  &e{player} &7- &fEnabled"
  list-empty: "  &7No players have PlaceAnywhere enabled."

storage:
  # YAML = saves data in a .yml file
  # NONE = no persistent storage
  type: YAML
  file: playerdata.yml
```

### Important options details

**`default-mode`**  
- `TOGGLE`: PlaceAnywhere resets every time the player logs out. Useful for survival servers where you don’t want it left on accidentally.  
- `PERSISTENT`: The state is saved in `playerdata.yml` and restored on next login.

**`feedback-type`**  
- `ACTIONBAR`: message above the inventory bar (recommended).  
- `TITLE`: large on-screen title.  
- `CHAT`: standard chat message.  
- `ALL`: both chat and actionbar.

**`bypass-protection-plugins`**  
If enabled, PlaceAnywhere attempts to ignore protection checks from plugins like WorldGuard or GriefPrevention. Use with caution: it may allow placement in protected areas.

**`aggressive-mode`**  
When enabled, the plugin intercepts and cancels the vanilla placement event, then sets the block directly via API. Fixes cases where Minecraft doesn’t even fire the event (e.g. short grass on wood). Recommended to keep it `true`.

---

## Generated file structure

```
plugins/PlaceAnywhere/
├── config.yml       ← Main configuration
└── playerdata.yml   ← Persistent player data (only in PERSISTENT mode)
```

---

## Technical behavior

- The plugin intercepts `BlockCanBuildEvent`, `BlockPlaceEvent`, and `PlayerInteractEvent`.
- For tall plants (e.g. sunflower, tall grass), it automatically places the upper block as well.
- For torches, if the click occurs on a side wall, it uses the correct wall variant (e.g. `WALL_TORCH` instead of `TORCH`).
- Bamboo is placed without leaves (`Bamboo.Leaves.NONE`) for simplicity.
- Force-placed blocks are temporarily tracked internally to suppress vanilla physics events that would immediately remove them.
- In Survival mode, the item is properly consumed from the inventory.

---

## Compatibility

- **Paper 1.20+** (recommended)
- **Spigot 1.20+** (supported, but `BlockCanBuildEvent.getPlayer()` may return `null`)
- No required dependencies.
- Optionally compatible with WorldGuard and GriefPrevention (via `bypass-protection-plugins`).
