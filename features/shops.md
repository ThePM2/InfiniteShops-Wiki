# 🛒 Shop System

The core feature of InfiniteShops - create beautiful, customizable GUI shops!

---

## Overview

The shop system allows you to create categorized GUI menus where players can buy and sell items. Each shop is defined in a YAML file and can be fully customized.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a beautifully designed shop menu with multiple categories and items. Dimensions: 800x500px -->

---

## Creating a Shop

### Basic Shop Structure

Create a new file in `plugins/InfiniteShops/shops/`:

```yaml
# shops/blocks.yml

# Shop display settings
title: '&2&lBlocks Shop'
rows: 6

# Menu layout (optional)
menu:
  - 'YYYYYYYYY'
  - 'Y       Y'
  - 'Y       Y'
  - 'Y       Y'
  - 'Y       Y'
  - 'YYYYYYYYY'

# Border items
replaces:
  Y: GREEN_STAINED_GLASS_PANE

# Shop items
items:
  dirt:
    material: DIRT
    slot: 10
    amount: 64
    buy_price: 10
    sell_price: 5
    ecoType: VAULT
```

---

## Item Configuration

### Basic Item

```yaml
items:
  diamond:
    material: DIAMOND
    slot: 13
    buy_price: 1000
    sell_price: 500
    ecoType: VAULT
```

### Advanced Item with Custom Display

```yaml
items:
  special_sword:
    # The actual item given to player
    material: DIAMOND_SWORD
    slot: 22
    amount: 1
    
    # Custom display settings
    display_name: '&b&lFrost Blade'
    lore:
      - '&7A legendary blade of ice'
      - ''
      - '&eClick to purchase!'
    
    # Enchantments
    enchantments:
      SHARPNESS: 5
      UNBREAKING: 3
    
    # Economy settings
    buy_price: 50000
    sell_price: null  # Cannot be sold
    ecoType: VAULT
    
    # Item flags
    item_flags:
      - HIDE_ENCHANTS
      - HIDE_ATTRIBUTES
```

### Item with Commands

```yaml
items:
  vip_rank:
    material: NETHER_STAR
    slot: 13
    display_name: '&6&lVIP Rank'
    lore:
      - '&7Purchase VIP status!'
      - ''
      - '&eBuy Price: &6$10,000'
    buy_price: 10000
    ecoType: VAULT
    
    # Execute commands on purchase
    commands:
      - 'lp user %player% parent set vip'
      - 'broadcast &a%player% &7purchased &6VIP&7!'
    command_executor: CONSOLE  # or PLAYER
```

---

## Economy Types

InfiniteShops supports multiple economy types per item:

| EcoType | Description | Example |
|---------|-------------|---------|
| `VAULT` | Standard Vault economy | `$500` |
| `EXP` | Experience points/levels | `100 XP` |
| `ITEM` | Trade for items | `10 Diamonds` |
| `CUSTOM` | Custom currency | `500 Gems` |
| `PLAYERPOINTS` | PlayerPoints plugin | `100 Points` |
| `TOKENENCHANT` | TokenEnchant tokens | `50 Tokens` |

### Using EXP as Currency

```yaml
items:
  enchanted_book:
    material: ENCHANTED_BOOK
    slot: 10
    buy_price: 30
    ecoType: EXP
    level: true  # Use levels instead of points
```

### Using Items as Currency

```yaml
items:
  beacon:
    material: BEACON
    slot: 13
    buy_price: 64
    sell_price: 32
    ecoType: ITEM
    currency_material: DIAMOND  # Pay with diamonds
```

### Combined Economy (AND/OR)

```yaml
items:
  legendary_item:
    material: NETHERITE_SWORD
    slot: 13
    ecoType: AND  # Requires BOTH
    prices:
      - type: VAULT
        amount: 100000
      - type: ITEM
        material: NETHER_STAR
        amount: 5
```

---

## Shop Categories

Create a main menu that links to other shops:

```yaml
# shops/main.yml
title: '&8&lShop Categories'
rows: 3

items:
  blocks:
    material: GRASS_BLOCK
    slot: 10
    display_name: '&a&lBlocks'
    lore:
      - '&7Buy building materials'
    action: OPEN_SHOP
    value: blocks
    
  tools:
    material: DIAMOND_PICKAXE
    slot: 12
    display_name: '&b&lTools'
    lore:
      - '&7Buy tools and equipment'
    action: OPEN_SHOP
    value: tools
    
  food:
    material: COOKED_BEEF
    slot: 14
    display_name: '&6&lFood'
    lore:
      - '&7Buy food items'
    action: OPEN_SHOP
    value: food
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a shop category menu with icons for different shop types. Dimensions: 600x400px -->

---

## Click Actions

Configure what happens when players click items:

### Default Actions

```yaml
# In config.yml
shop_actions:
  LEFT:
    action: BUY
    identifier: 'Left click:'
    description: 'Buy %amount% for %price%'
  RIGHT:
    action: SELL
    identifier: 'Right click:'
    description: 'Sell %amount% for %price%'
  SHIFT_LEFT:
    action: BUY_STACK
    identifier: 'Shift + Left:'
    description: 'Buy 64 for %price%'
  SHIFT_RIGHT:
    action: SELL_ALL
    identifier: 'Shift + Right:'
    description: 'Sell all for %price%'
```

### Available GUI Actions

| Action | Description |
|--------|-------------|
| `BUY` | Buy the item amount |
| `SELL` | Sell the item amount |
| `BUY_STACK` | Buy a full stack (64) |
| `SELL_ALL` | Sell all matching items |
| `OPEN_SHOP` | Open another shop |
| `PLAYER_COMMAND` | Run command as player |
| `CONSOLE_COMMAND` | Run command as console |
| `CLOSE` | Close the menu |

---

## Multi-Page Shops

For shops with many items, pagination is automatic:

```yaml
title: '&8All Items'
rows: 6

# Pagination buttons (auto-placed on last row)
pagination:
  next:
    material: ARROW
    name: '&aNext Page →'
  previous:
    material: ARROW
    name: '&c← Previous Page'
  
items:
  # Define many items - pages are created automatically
  item1:
    material: STONE
    buy_price: 1
  item2:
    material: COBBLESTONE
    buy_price: 2
  # ... more items
```

<!-- 📸 GIF PLACEHOLDER: Animation showing pagination in action - clicking next/previous page buttons. Dimensions: 600x400px -->

---

## Preview System

Allow players to preview items before purchasing:

```yaml
# In config.yml
preview:
  enabled: true
  name: '&aPreview item'
  name_shulker: '&5Preview shulker content'
  size: 5
  menu:
    - 'LY     YL'
    - 'Y       Y'
    - 'L       L'
    - 'Y       Y'
    - 'LY     YL'
  replaces:
    Y: YELLOW_STAINED_GLASS_PANE
    L: LIME_STAINED_GLASS_PANE
```

---

## Search Function

Players can search for items across all shops:

```
/shop search <query>
```

<!-- 📸 GIF PLACEHOLDER: Animation showing the search functionality - typing a query and results appearing. Dimensions: 600x400px -->

---

## Tips & Best Practices

1. **Organize by category** - Create logical shop groupings
2. **Use consistent pricing** - Sell prices should be lower than buy prices
3. **Add visual borders** - Use glass panes for professional look
4. **Include descriptions** - Help players understand items
5. **Test thoroughly** - Verify all items work correctly

---

## Related Features

- [Limited Stock](../economy/dynamic-pricing.md) - Limit item availability
- [Taxes](../economy/taxes-discounts.md) - Apply taxes to transactions
- [Multipliers](../economy/multipliers.md) - Give VIP price bonuses
