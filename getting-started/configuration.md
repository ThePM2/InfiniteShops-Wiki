# ⚙️ Basic Configuration

Learn how to configure InfiniteShops to match your server's needs.

---

## Configuration Files Overview

InfiniteShops uses multiple configuration files for different features:

| File | Purpose |
|------|---------|
| `config.yml` | Main plugin settings |
| `messages.yml` | All text messages and translations |
| `permissions.yml` | Permission node definitions |
| `shops/*.yml` | Individual shop categories |

---

## Main Config (config.yml)

The `config.yml` file contains all core plugin settings.

### General Settings

```yaml
# Debug mode - only enable when troubleshooting
debug: false

# Hologram plugin to use (auto-detected if empty)
# Options: DecentHolograms, HolographicDisplays, CMI, etc.
hologram-handler: ""

# Database settings
database:
  type: SQLite  # SQLite or MySQL
  # MySQL settings (if using MySQL)
  host: localhost
  port: 3306
  database: infiniteshops
  username: root
  password: ""
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of the config.yml file in a text editor with syntax highlighting. Dimensions: 800x500px -->

### Shop Settings

```yaml
shop:
  # Economy type placeholders
  ecoType_placeholders:
    VAULT: "$"
    EXP: " XP"
    CUSTOM: " points"
    NOT_ENABLED: ""
  
  # Preview settings
  preview:
    enabled: true
    size: 5  # rows
```

### Sound Effects

```yaml
sounds:
  buy: ENTITY_EXPERIENCE_ORB_PICKUP
  sell: ENTITY_EXPERIENCE_ORB_PICKUP
  sellall: ENTITY_PLAYER_LEVELUP
  error: ENTITY_VILLAGER_NO
  click: UI_BUTTON_CLICK
```

---

## Feature Toggles

Enable or disable features in `config.yml`:

```yaml
features:
  black-market: true
  daily-shop: true
  custom-currencies: true
  loot: true
  multipliers: true
  sign-shops: true
  shopper-rank: true
  item-discount: true
  stack-discount: true
  taxes: true
  dynamic-pricing: false
  frame-shop: true
  player-frame-shop: true
  limited-stock: true
  limited-sell: false
  npc: true
  realistic-season: false
  transaction-logging: true
```

Use `/ishop toggle <feature>` to toggle features in-game.

<!-- 📸 GIF PLACEHOLDER: Animation showing the /ishop toggle command enabling and disabling a feature. Dimensions: 600x300px -->

---

## Shop Buttons

Configure global buttons that appear in all shop menus:

```yaml
buttons:
  showCurrency:
    display_item: CLOCK
    name: '&7You have &6&l%vault_eco_balance_formatted%'
    slot: 'LAST - 2'
  
  back:
    display_item: BARRIER
    name: '&cBack'
    slot: LAST
    action: PLAYER_COMMAND
    value: ishop
  
  search:
    display_item: OAK_SIGN
    name: '&cSearch'
    slot: 'LAST - 1'
    action: SEARCH
```

### Available Actions

| Action | Description |
|--------|-------------|
| `PLAYER_COMMAND` | Execute a command as player |
| `CONSOLE_COMMAND` | Execute a command as console |
| `SEARCH` | Open the search interface |
| `CLOSE` | Close the inventory |
| `NEXT_PAGE` | Go to next page |
| `PREVIOUS_PAGE` | Go to previous page |

---

## Creating Your First Shop

### Step 1: Create a Shop File

Create a new file in `plugins/InfiniteShops/shops/`:

```yaml
# shops/tools.yml
title: '&8Tools Shop'
rows: 3

items:
  wooden_pickaxe:
    material: WOODEN_PICKAXE
    slot: 10
    buy_price: 50
    sell_price: 10
    ecoType: VAULT
    
  stone_pickaxe:
    material: STONE_PICKAXE
    slot: 11
    buy_price: 100
    sell_price: 25
    ecoType: VAULT
    
  iron_pickaxe:
    material: IRON_PICKAXE
    slot: 12
    buy_price: 500
    sell_price: 100
    ecoType: VAULT
```

### Step 2: Reload the Plugin

```
/ishop reload
```

### Step 3: Open Your Shop

```
/shop tools
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing a populated tools shop GUI in-game with items and prices. Dimensions: 600x400px -->

---

## In-Game Editor

InfiniteShops includes a powerful in-game shop editor:

```
/ishop editor
```

<!-- 📸 GIF PLACEHOLDER: Animation showing the shop editor interface - adding items, setting prices, and saving. Dimensions: 700x450px -->

The editor allows you to:
- Create and edit shop categories
- Add/remove/modify items
- Set prices and economy types
- Configure item lore and display names
- Set slot positions

---

## Quick Configuration Tips

1. **Always backup** your config files before making changes
2. **Use `/ishop reload`** after modifying configuration files
3. **Test changes** on a development server first
4. **Validate YAML** syntax using an online validator
5. **Use consistent naming** for shop files (lowercase, no spaces)

---

## Next Steps

- [Configure the Black Market](../features/black-market.md)
- [Set up currencies](../economy/currencies.md)
- [Learn about commands](../commands-permissions/commands.md)
