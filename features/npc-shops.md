# 👤 NPC Shops

Create immersive merchant NPCs using Citizens integration!

---

## Overview

NPC Shops allow you to create interactive villager or custom NPCs that act as shop keepers. Players can interact with NPCs to open shop menus, creating an immersive trading experience.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing multiple NPC merchants in a marketplace setting with name tags and different skins. Dimensions: 800x450px -->

---

## Requirements

NPC Shops require the **Citizens** plugin:

- [Download Citizens](https://www.spigotmc.org/resources/citizens.13811/)

---

## Creating NPC Shops

### Method 1: Using the NPC Create Command

```
/ishop npc create
```

This opens an interactive setup menu:

<!-- 📸 GIF PLACEHOLDER: Animation showing the NPC creation menu - selecting type, setting name, linking shop. Dimensions: 600x400px -->

### Method 2: Link Existing NPC

1. Select an existing Citizens NPC:
```
/npc select
```

2. Link it to a shop:
```
/ishop npc link <shopName>
```

### Method 3: Create with Parameters

```
/ishop npc create VILLAGER tools "Tool Merchant"
```

Parameters:
- Entity Type (VILLAGER, PLAYER, etc.)
- Shop name (from your shops folder)
- Display name

---

## NPC Configuration

### Basic NPC Settings

```yaml
# In config.yml

npc:
  # Enable teleport to NPC on click
  teleport: true
  
  # Click actions
  clicks:
    RIGHT: OPEN_SHOP
    LEFT: INFO
    SHIFT_RIGHT: TELEPORT  # Admin only
```

### Per-NPC Configuration

Each NPC can have custom settings:

```
/ishop npc settings
```

Opens the NPC settings GUI:

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of NPC settings GUI showing options like shop link, entity type, hologram settings. Dimensions: 500x400px -->

---

## Entity Types

InfiniteShops supports all Citizens entity types:

| Type | Description |
|------|-------------|
| `VILLAGER` | Classic villager NPC |
| `PLAYER` | Player NPC with custom skin |
| `ZOMBIE` | Zombie NPC |
| `SKELETON` | Skeleton NPC |
| `WITCH` | Witch NPC |
| `WANDERING_TRADER` | Wandering trader |
| *Any mob* | Citizens supports most mobs |

### Setting Entity Type

```
/ishop npc type WANDERING_TRADER
```

Or use the settings GUI.

---

## NPC Holograms

Display information above NPCs:

```yaml
npc:
  hologram:
    enabled: true
    height: 2.5
    lines:
      - '&6&l%npc_name%'
      - '&7Click to open shop'
      - '&e%shop_name%'
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of an NPC with hologram text floating above showing name and shop info. Dimensions: 400x350px -->

---

## NPC Interactions

### Click Actions

Configure what happens on different clicks:

```yaml
npc:
  clicks:
    RIGHT: OPEN_SHOP      # Open linked shop
    LEFT: INFO            # Show NPC info
    SHIFT_RIGHT: TELEPORT # Teleport (admin)
    SHIFT_LEFT: DELETE    # Delete NPC (admin)
```

### Available Actions

| Action | Description |
|--------|-------------|
| `OPEN_SHOP` | Opens the linked shop |
| `INFO` | Shows NPC information |
| `TELEPORT` | Teleports player to NPC |
| `DELETE` | Removes the NPC |
| `COMMAND` | Runs a command |

---

## NPC List Management

### View All NPCs

```
/ishop npc list
```

Opens a GUI showing all NPC shops:

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of NPC list GUI showing multiple NPCs with their types, shops, and locations. Dimensions: 600x400px -->

### Teleport to NPC

From the list, click an NPC to teleport to it (with permission).

### Remove NPC

```
/ishop npc remove <id>
```

Or left-click in the NPC list (admin only).

---

## Advanced Configuration

### Merchant Trades (Villager-style)

Create villager-like trading interfaces:

```yaml
# In npc config
merchant:
  enabled: true
  trades:
    - input:
        material: EMERALD
        amount: 10
      output:
        material: DIAMOND
        amount: 1
    - input:
        material: WHEAT
        amount: 20
      output:
        material: EMERALD
        amount: 1
```

<!-- 📸 GIF PLACEHOLDER: Animation showing a merchant trade interface similar to vanilla villager trading. Dimensions: 600x350px -->

### NPC Animations

Configure NPC behaviors:

```yaml
npc:
  animations:
    look_at_player: true
    idle_animation: true
    particle_effect: HAPPY_VILLAGER
```

---

## Commands Reference

| Command | Description |
|---------|-------------|
| `/ishop npc create` | Open NPC creation menu |
| `/ishop npc create <type> <shop> [name]` | Quick create NPC |
| `/ishop npc link <shop>` | Link selected NPC to shop |
| `/ishop npc unlink` | Remove shop link |
| `/ishop npc list` | View all NPC shops |
| `/ishop npc remove <id>` | Remove an NPC |
| `/ishop npc settings` | Open NPC settings |
| `/ishop npc type <type>` | Change entity type |
| `/ishop npc teleport <id>` | Teleport to NPC |

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.npc` | Create/manage NPCs | op |
| `infiniteshops.npc.menu` | Access NPC list | op |
| `infiniteshops.npc.settings` | Modify NPC settings | op |
| `infiniteshops.npc.teleport` | Teleport to NPCs | op |

---

## Troubleshooting

### NPC Not Opening Shop

1. Verify shop file exists
2. Check NPC is linked: `/ishop npc info`
3. Verify player has shop permissions
4. Check Citizens is properly installed

### Invalid Entity Type

Ensure the entity type is valid for Citizens. Check Citizens documentation for supported types.

### NPC Not Spawning

1. Check spawn location is valid
2. Verify chunk is loaded
3. Check Citizens spawn settings

---

## Tips

1. **Use player NPCs** for custom skins
2. **Position NPCs** in logical market areas
3. **Add holograms** for clear identification
4. **Use different entity types** for different shop categories
5. **Test permissions** to ensure players can interact
