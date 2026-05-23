# DemonSlayer / DMS

Immersive Demon Slayer inspired gameplay plugin for Spigot/Paper 1.21.1.

DMS adds player origins, breathing styles, Blood Demon Arts, custom items, combo-based ability execution, boss encounters, atmospheric effects, and a procedurally generated Infinity Castle world.

## Features

- Human and Demon player origins
- Breathing style progression with unlockable forms
- Blood Demon Art abilities for many demon archetypes
- Combo editor GUI with configurable input sequences
- Custom item system backed by `custom_items.yml`
- Nichirin Blade requirement for breathing techniques
- Boss encounters for Rui, Enmu, Swamp Demon, Hand Demon, and Hantengu
- Infinity Castle world generation with shifting rooms and gravity gates
- Optional SQLite player-data backend
- Join atmosphere, Kasugai Crow messages, and ambient aura effects
- Admin GUI for player class, demon type, breathing, and form management

## Requirements

- Minecraft server: Spigot or Paper compatible with API `1.21`
- Java compatible with your server runtime
- Optional: Citizens, used by selected NPC/boss systems

The plugin declares Citizens as a soft dependency, so the server can start without it, but Citizens-backed boss/NPC behavior may be limited.

## Building

From the project root:

```powershell
.\gradlew.bat build
```

The compiled plugin jar is generated under:

```text
build/libs/
```

## Installation

1. Build the plugin.
2. Copy the generated jar from `build/libs/` into your server `plugins/` folder.
3. Start the server once to generate configuration files.
4. Adjust `config.yml`, `commands.yml`, `custom_items.yml`, and `messages.yml`.
5. Restart the server or use `/dms reload` where appropriate.

## Commands

Main command aliases:

- `/dms`
- `/demon`
- `/demonslayer`

Standalone combo command:

- `/combo`
- `/combomanager`

Subcommands:

| Command | Description | Permission |
| --- | --- | --- |
| `/dms profile <setclass\|setdemontype\|unlock...>` | Manage player classes, demon types, and unlocks | `demon.dms` |
| `/dms reload` | Reload configuration, messages, items, commands, and runtime listeners | `demon.reload` |
| `/dms reloadcommands` | Reload command metadata from `commands.yml` | `demon.commands.reload` |
| `/dms createtrainer` | Spawn a trainer villager at your location | `demon.createtrainer` |
| `/dms removetrainer` | Remove the nearest trainer villager | `demon.removetrainer` |
| `/dms playermenu` | Open your player menu | `demon.playermenu` |
| `/dms adminmenu <player>` | Open the admin editor for a player | `demon.adminmenu` |
| `/dms totalconcentration` | Open Total Concentration training | `demon.totalconcentration` |
| `/dms meditation` | Start meditation training | `demon.meditation` |
| `/dms breathing [list\|unlock\|use]` | Manage breathing techniques | `demon.breathing` |
| `/dms blooddemonart` | Spawn/use Blood Demon Art tooling | `demon.sk` |
| `/dms infinity [reset]` | Enter or reset the Infinity Castle | `demon.icastle` |
| `/dms boss <rui\|swamp\|enmu\|hand\|hantengu>` | Summon boss encounters | `demon.boss` |
| `/dms giveitem <player> <item_id> [amount]` | Give configured custom items | `demon.giveitem` |
| `/dms event <event> [args...]` | Trigger custom DMS events | `demon.event` |
| `/combo` | Open the combo editor GUI | `demon.combo.use` |

## Permissions

Common player permissions:

- `demon.breathing`
- `demon.playermenu`
- `demon.combo.use`
- `demon.totalconcentration`
- `demon.meditation`

Common admin permissions:

- `demon.dms`
- `demon.dms.unlock`
- `demon.adminmenu`
- `demon.reload`
- `demon.commands.reload`
- `demon.boss`
- `demon.giveitem`
- `demon.event`
- `demon.createtrainer`
- `demon.removetrainer`
- `demon.sk`
- `demon.icastle`

Admin bundle:

- `demon.dms.admin`

## Configuration Files

### `config.yml`

Main runtime configuration:

- Plugin prefix
- Player data backend
- Infinity Castle generation settings
- Atmosphere effects
- Kasugai Crow messages
- Ambient aura particles and sounds
- Combo slot sequences and limits

Player data storage:

```yaml
player-data:
  use-sqlite: true
```

- `false`: stores player data as YAML files in `plugins/DMS/playerdata`
- `true`: stores player data in `plugins/DMS/playerdata.db`

### `commands.yml`

Allows server owners to override command metadata:

- Permission node
- Usage text
- Description
- Aliases

### `custom_items.yml`

Defines custom items used by the plugin.

Important item IDs include:

- `nichirin_blade`
- `wisteria_sword`
- `slayer_blade`
- `wisteria_potion`
- `demon_blood_vial`
- `breathing_scroll`

Breathing techniques require the configured Nichirin Blade. Normal Minecraft swords are intentionally not accepted for breathing usage.

Give an item with:

```text
/dms giveitem <player> nichirin_blade 1
```

### `messages.yml`

Contains configurable user-facing messages.

## Combo System

Players can open the combo editor with:

```text
/combo
```

Default combo slot sequences are configured in `config.yml`:

```yaml
combo:
  slotSequences:
    - "R-L-R"
    - "L-L-R"
    - "R-R-L"
    - "L-R-L"
    - "R-L-L"
```

`R` means right click and `L` means left click. Assigned abilities are executed when the player performs a matching sequence.

## Infinity Castle

The Infinity Castle is generated as a separate world, configured by:

```yaml
plugin:
  infinityWorldName: "infinityWorld"
```

Generation behavior is controlled under:

```yaml
infinityCastle:
```

After changing major generation settings, reset the generated world with:

```text
/dms infinity reset
```

## Development Notes

The project uses Gradle with the Shadow plugin.

Primary dependencies:

- Spigot API `1.21.1-R0.1-SNAPSHOT`
- Citizens API `2.0.40-SNAPSHOT`
- SQLite JDBC

Useful commands:

```powershell
.\gradlew.bat build
.\gradlew.bat clean build
```

## Current Stability Notes

- Boss listener registration is centralized to avoid duplicate event handling.
- Runtime combo listeners are re-registered after `/dms reload`.
- Boss cleanup is called on reload/disable to prevent stale boss tasks from continuing.
- Existing particle-heavy ability animations are intentionally preserved for the anime-style visual impact.


<img width="1920" height="1009" alt="2025-06-22_17 50 32" src="https://github.com/user-attachments/assets/738f63a2-4cb3-49c3-8c9b-d5d2aca78508" />
<img width="1920" height="1009" alt="2025-06-19_11 49 41" src="https://github.com/user-attachments/assets/7934ff25-dbe7-4feb-9208-84b0277150e1" />
<img width="1920" height="1009" alt="2025-06-18_23 25 29" src="https://github.com/user-attachments/assets/eaa35567-625b-4515-85ae-e44ea8b69814" />
<img width="1920" height="1009" alt="2025-06-18_21 18 39" src="https://github.com/user-attachments/assets/da28b3bf-a867-4d46-82cf-22d1ac5567c3" />
<img width="1920" height="1009" alt="2025-06-16_19 26 45" src="https://github.com/user-attachments/assets/cb531f5f-b0f1-4b44-bcf7-4118dec43412" />
<img width="1920" height="1009" alt="2025-06-16_18 57 18" src="https://github.com/user-attachments/assets/d0b9679d-93d3-40d4-a0d7-6b2043f0225f" />
<img width="1920" height="1009" alt="2025-06-16_18 57 17" src="https://github.com/user-attachments/assets/9759da54-6029-4cb3-afe1-58a3411518e4" />
<img width="1920" height="1009" alt="2025-06-15_13 26 55" src="https://github.com/user-attachments/assets/be8ff030-3c04-4c71-91fa-68831e1540ec" />


