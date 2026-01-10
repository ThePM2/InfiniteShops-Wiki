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

# Shop category settings
name: '&2&lBlocks Shop'
size: 54  # Inventory size in slots (9, 18, 27, 36, 45, or 54)
category_display_item: GRASS_BLOCK  # Icon shown in main menu
lore:
  - ''
  - '&a➼ &fOpen the Blocks shop'
  - ''

# Shop items
items:
  dirt1:
    itemType: ITEM
    display_item:
      type: DIRT
      amount: 1
    slot: 10
    show: true
    item:
      type: DIRT
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 10.0
      sellPrice: 5.0
```

---

## Item Configuration

### Basic Sellable Item

```yaml
items:
  diamond1:
    itemType: ITEM
    display_item:
      type: DIAMOND
      amount: 1
    slot: 13
    show: true
    item:
      type: DIAMOND
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 1000.0
      sellPrice: 500.0
```

### Item with Custom Display Name and Lore

```yaml
items:
  special_sword1:
    itemType: ITEM
    display_item:
      type: DIAMOND_SWORD
      amount: 1
      display_name: '&b&lFrost Blade'
      lore:
        - '&7A legendary blade of ice'
        - ''
        - '&eClick to purchase!'
    slot: 22
    show: true
    item:
      type: DIAMOND_SWORD
      amount: 1
      display_name: '&b&lFrost Blade'
      lore:
        - '&7A legendary blade of ice'
      enchants:
        1:
          enchant: SHARPNESS
          level: 5
        2:
          enchant: UNBREAKING
          level: 3
    shop:
      ecoType: VAULT
      buyPrice: 50000.0
      sellPrice: null  # Cannot be sold (use null or omit)
```

### Item Types

| itemType | Description |
|----------|-------------|
| `ITEM` | Standard buyable/sellable item |
| `BUTTON` | Navigation button (opens menus, runs commands) |
| `FILLER` | Decorative item (glass panes, etc.) |
| `COMMAND` | Executes commands on purchase |
| `ENCHANT` | Enchantment book item |

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
| `OR` | Either currency option | `$500 OR 10 Diamonds` |
| `AND` | Both currencies required | `$500 AND 10 Diamonds` |

### Using EXP as Currency

```yaml
items:
  enchanted_book1:
    itemType: ITEM
    display_item:
      type: ENCHANTED_BOOK
      amount: 1
    slot: 10
    show: true
    item:
      type: ENCHANTED_BOOK
      amount: 1
    shop:
      ecoType: EXP
      buyPrice: 30.0
```

### Using Items as Currency

```yaml
items:
  beacon1:
    itemType: ITEM
    display_item:
      type: BEACON
      amount: 1
    slot: 13
    show: true
    item:
      type: BEACON
      amount: 1
    shop:
      ecoType: ITEM
      buyPrice: 64.0
      sellPrice: 32.0
      # Currency item defined in currencies configuration
```

---

## Navigation Buttons

### Opening Other Shop Categories

```yaml
items:
  blocks_button:
    itemType: BUTTON
    display_item:
      type: GRASS_BLOCK
      amount: 1
      display_name: '&a&lBlocks'
      lore:
        - ''
        - '&7Click to open the Blocks shop'
        - ''
    slot: 10
    show: true
    button:
      action: OPEN_MENU
      value: blocks  # Shop file name without .yml

  tools_button:
    itemType: BUTTON
    display_item:
      type: DIAMOND_PICKAXE
      amount: 1
      display_name: '&b&lTools'
      lore:
        - ''
        - '&7Click to open the Tools shop'
        - ''
    slot: 12
    show: true
    button:
      action: OPEN_MENU
      value: tools
```

### Button Actions

| Action | Description |
|--------|-------------|
| `OPEN_MENU` | Open another shop category |
| `PLAYER_COMMAND` | Run command as player |
| `CONSOLE_COMMAND` | Run command as console |
| `CLOSE` | Close the menu |
| `SEARCH` | Open search interface |

### Navigation with Player Heads

```yaml
items:
  next_category:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvN2M2MDJkYmE5Zjk3MDFhZTAwMzllNzQ4MWNlYmY2MWM1OGZlOGQzOWQyOWM5MjdiNDg4YmVlNDIyZDlhNjJkNCJ9fX0=
      display_name: '&a⇨ &fNext Category'
      lore:
        - ''
        - '&a➼ &fOpen the Farm shop'
        - ''
      amount: 1
    slot: 8
    show: true
    button:
      action: OPEN_MENU
      value: farm
```

---

## Filler Items (Decorations)

```yaml
items:
  glass_border:
    itemType: FILLER
    display_item:
      type: BLACK_STAINED_GLASS_PANE
      amount: 1
      display_name: ' '
    slot:
      - '0'
      - '8'
      - '45'
      - '53'
    show: true
```

---

## Click Actions

Configure what happens when players click items in `config.yml`:

```yaml
actions:
  ITEM:
    LEFT:
      action: OPEN_MULTIPLE_BUY
      identifier: 'Left click:'
      description: 'Open buy multiple'
    RIGHT:
      action: OPEN_MULTIPLE_SELL
      identifier: 'Right click:'
      description: 'Open sell multiple'
    SHIFT_LEFT:
      action: SELL_ALL
      identifier: 'Shift-Left Click:'
      description: 'Sell all'
```

### Available GUI Actions

| Action | Description |
|--------|-------------|
| `BUY` | Buy the item |
| `SELL` | Sell the item |
| `SELL_ALL` | Sell all matching items from inventory |
| `OPEN_MULTIPLE_BUY` | Open quantity selection for buying |
| `OPEN_MULTIPLE_SELL` | Open quantity selection for selling |
| `BUY_STACKS` | Open stack buying menu |
| `SELL_STACKS` | Open stack selling menu |
| `EXIT` | Close the menu |
| `BACK` | Go back to previous menu |

---

## Multi-Page Shops

For shops with many items, use navigation buttons to link pages:

```yaml
# shops/blocks.yml - Page 1
items:
  next_page:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcy...  # Arrow texture
      display_name: '&a⇨ &fGo to next page'
      amount: 1
    slot: 52
    show: true
    button:
      action: OPEN_MENU
      value: blocks2  # Links to blocks2.yml
```

```yaml
# shops/blocks2.yml - Page 2
items:
  previous_page:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcy...  # Arrow texture
      display_name: '&a⇦ &fGo to previous page'
      amount: 1
    slot: 50
    show: true
    button:
      action: OPEN_MENU
      value: blocks
```

<!-- 📸 GIF PLACEHOLDER: Animation showing pagination in action - clicking next/previous page buttons. Dimensions: 600x400px -->

---

## Preview System

Allow players to preview items before purchasing. Configure in `config.yml`:

```yaml
player_item_frame:
  preview:
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
    single_item_slot: 22
    shulker_preview: [2, 3, 4, 5, 6, 10, 11, 12, 13, 14, 15, 16, 19, 20, 21, 22, 23, 24, 25, 28, 29, 30, 31, 32, 33, 34, 40]
```

---

## Search Function

Players can search for items across all shops:

```
/shop search <query>
```

<!-- 📸 GIF PLACEHOLDER: Animation showing the search functionality - typing a query and results appearing. Dimensions: 600x400px -->

---

## Complete Shop Example

```yaml
# shops/tools.yml
name: '&7&m   &7] &6&lTools &7[&m   '
size: 54
category_display_item: DIAMOND_PICKAXE
lore:
  - ''
  - '&a➼ &fOpen the Tools shop'
  - ''

items:
  # Navigation
  previous_category:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvZGUxZGZjMTFhODM3MTExZDIyYjAwMWExNDQ2MWY5YTdmYzA5MzUyMmY4OGM1OGZhZWZkNmFkZWZmY2Q0ZTlhYiJ9fX0=
      display_name: '&a⇦ &fPrevious Category'
      amount: 1
    slot: 0
    show: true
    button:
      action: OPEN_MENU
      value: blocks

  next_category:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvN2M2OWQ0MTA3NmE4ZGVhNGYwNmQzZjFhOWFjNDdjYzk5Njk4OGI3NGEwOTEzYWIyYWMxYTc0Y2FmNzA4MTkxOCJ9fX0=
      display_name: '&a⇨ &fNext Category'
      amount: 1
    slot: 8
    show: true
    button:
      action: OPEN_MENU
      value: food

  # Decorative border
  border:
    itemType: FILLER
    display_item:
      type: GRAY_STAINED_GLASS_PANE
      amount: 1
      display_name: ' '
    slot:
      - '1'
      - '7'
    show: true

  # Shop items
  wooden_pickaxe1:
    itemType: ITEM
    display_item:
      type: WOODEN_PICKAXE
      amount: 1
    slot: 18
    show: true
    item:
      type: WOODEN_PICKAXE
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 50.0
      sellPrice: 5.0

  stone_pickaxe1:
    itemType: ITEM
    display_item:
      type: STONE_PICKAXE
      amount: 1
    slot: 19
    show: true
    item:
      type: STONE_PICKAXE
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 100.0
      sellPrice: 10.0

  iron_pickaxe1:
    itemType: ITEM
    display_item:
      type: IRON_PICKAXE
      amount: 1
    slot: 20
    show: true
    item:
      type: IRON_PICKAXE
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 500.0
      sellPrice: 50.0

  diamond_pickaxe1:
    itemType: ITEM
    display_item:
      type: DIAMOND_PICKAXE
      amount: 1
    slot: 21
    show: true
    item:
      type: DIAMOND_PICKAXE
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 2500.0
      sellPrice: 250.0
```

---

## Tips & Best Practices

1. **Use unique item names** - Add numbers or suffixes to item keys (e.g., `dirt1`, `stone1`)
2. **Always include `itemType`** - Required for all items
3. **Use `show: true`** - Items won't display without this
4. **Match display_item and item** - Keep them consistent for clarity
5. **Use camelCase for prices** - `buyPrice` and `sellPrice`, not `buy_price`
6. **Wrap prices in `shop:` section** - Required structure for economy settings
7. **Test after changes** - Use `/ishop reload` to apply changes

---

## Related Features

- [Limited Stock](../economy/dynamic-pricing.md) - Limit item availability
- [Taxes](../economy/taxes-discounts.md) - Apply taxes to transactions
- [Multipliers](../economy/multipliers.md) - Give VIP price bonuses
