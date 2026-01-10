# 🛒 Shop Configuration

Detailed reference for shop YAML file structure.

---

## File Location

Shop files are stored in: `plugins/InfiniteShops/shops/`

Each `.yml` file in this folder defines a shop category.

---

## Shop File Structure

```yaml
# Root-level settings
name: '&6&lShop Name'           # Display title in GUI
size: 54                         # Inventory size (9, 18, 27, 36, 45, 54)
category_display_item: DIAMOND   # Icon in main menu
lore:                            # Description shown in main menu
  - ''
  - '&a➼ &fClick to open this shop'
  - ''
permission: 'shop.category.name' # Optional permission requirement

# Items section
items:
  item_key:
    # Item configuration here
```

---

## Item Types

### ITEM - Buyable/Sellable Items

```yaml
items:
  diamond1:
    itemType: ITEM
    display_item:
      type: DIAMOND
      amount: 1
      display_name: '&bDiamond'  # Optional
      lore:                       # Optional
        - '&7A precious gem'
    slot: 10
    show: true
    item:
      type: DIAMOND
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 1000.0
      sellPrice: 500.0
```

### BUTTON - Navigation Elements

```yaml
items:
  next_page:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6...  # Base64 skin
      display_name: '&aNext Page →'
      amount: 1
    slot: 53
    show: true
    button:
      action: OPEN_MENU
      value: shop_page2
```

### FILLER - Decorative Items

```yaml
items:
  border:
    itemType: FILLER
    display_item:
      type: BLACK_STAINED_GLASS_PANE
      amount: 1
      display_name: ' '
    slot:
      - '0'
      - '1'
      - '2'
    show: true
```

### COMMAND - Execute Commands

```yaml
items:
  vip_purchase:
    itemType: COMMAND
    display_item:
      type: NETHER_STAR
      amount: 1
      display_name: '&6&lVIP Rank'
      lore:
        - '&7Purchase VIP status!'
    slot: 22
    show: true
    shop:
      ecoType: VAULT
      buyPrice: 10000.0
    commands:
      - 'lp user %player% parent set vip'
      - 'broadcast &a%player% purchased VIP!'
```

### ENCHANT - Enchantment Books

```yaml
items:
  sharpness_book:
    itemType: ENCHANT
    display_item:
      type: ENCHANTED_BOOK
      amount: 1
      display_name: '&aSharpness V'
    slot: 13
    show: true
    item:
      type: ENCHANTED_BOOK
      amount: 1
      enchants:
        1:
          enchant: SHARPNESS
          level: 5
    shop:
      ecoType: VAULT
      buyPrice: 5000.0
```

---

## Display Item Properties

```yaml
display_item:
  type: DIAMOND_SWORD        # Material type (required)
  amount: 1                   # Stack size
  display_name: '&b&lName'   # Custom name
  lore:                       # Item description
    - '&7Line 1'
    - '&7Line 2'
  skin: 'base64...'          # For PLAYER_HEAD only
  customModelData: 1001      # Custom model data
```

---

## Item Properties

```yaml
item:
  type: DIAMOND_SWORD
  amount: 1
  display_name: '&b&lFrost Blade'
  lore:
    - '&7A legendary sword'
  enchants:
    1:
      enchant: SHARPNESS
      level: 5
    2:
      enchant: UNBREAKING
      level: 3
  item_flags:
    - HIDE_ENCHANTS
    - HIDE_ATTRIBUTES
  customModelData: 1001
```

---

## Shop Section (Economy)

```yaml
shop:
  ecoType: VAULT           # Economy type
  buyPrice: 1000.0         # Purchase price (null = cannot buy)
  sellPrice: 500.0         # Sell price (null = cannot sell)
```

### Economy Types

| Type | Description |
|------|-------------|
| `VAULT` | Standard server economy |
| `EXP` | Experience points |
| `ITEM` | Item currency |
| `CUSTOM` | Custom currency |
| `PLAYERPOINTS` | PlayerPoints plugin |
| `TOKENENCHANT` | TokenEnchant tokens |
| `OR` | Either option |
| `AND` | Both required |

---

## Button Actions

```yaml
button:
  action: OPEN_MENU      # Action type
  value: shop_name       # Action parameter
```

| Action | Description | Value |
|--------|-------------|-------|
| `OPEN_MENU` | Open another shop | Shop file name |
| `PLAYER_COMMAND` | Run as player | Command string |
| `CONSOLE_COMMAND` | Run as console | Command string |
| `CLOSE` | Close GUI | - |
| `SEARCH` | Open search | - |

---

## Slot Configuration

### Single Slot

```yaml
slot: 13
```

### Multiple Slots (for fillers)

```yaml
slot:
  - '0'
  - '1'
  - '2'
  - '8'
  - '9'
  - '17'
```

---

## Enchantment Format

```yaml
enchants:
  1:
    enchant: SHARPNESS     # Enchantment name
    level: 5               # Enchantment level
  2:
    enchant: UNBREAKING
    level: 3
  3:
    enchant: FIRE_ASPECT
    level: 2
```

---

## Complete Shop Example

```yaml
# shops/weapons.yml

name: '&c&lWeapons Shop'
size: 54
category_display_item: DIAMOND_SWORD
lore:
  - ''
  - '&a➼ &fBuy weapons and armor'
  - ''

items:
  # Navigation
  prev_category:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvZGUxZGZjMTFhODM3MTExZDIyYjAwMWExNDQ2MWY5YTdmYzA5MzUyMmY4OGM1OGZhZWZkNmFkZWZmY2Q0ZTlhYiJ9fX0=
      display_name: '&a⇦ &fPrevious'
      amount: 1
    slot: 0
    show: true
    button:
      action: OPEN_MENU
      value: tools

  next_category:
    itemType: BUTTON
    display_item:
      type: PLAYER_HEAD
      skin: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvN2M2OWQ0MTA3NmE4ZGVhNGYwNmQzZjFhOWFjNDdjYzk5Njk4OGI3NGEwOTEzYWIyYWMxYTc0Y2FmNzA4MTkxOCJ9fX0=
      display_name: '&a⇨ &fNext'
      amount: 1
    slot: 8
    show: true
    button:
      action: OPEN_MENU
      value: armor

  # Border
  glass_border:
    itemType: FILLER
    display_item:
      type: GRAY_STAINED_GLASS_PANE
      amount: 1
      display_name: ' '
    slot:
      - '1'
      - '7'
    show: true

  # Weapons
  wooden_sword1:
    itemType: ITEM
    display_item:
      type: WOODEN_SWORD
      amount: 1
    slot: 18
    show: true
    item:
      type: WOODEN_SWORD
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 25.0
      sellPrice: 5.0

  stone_sword1:
    itemType: ITEM
    display_item:
      type: STONE_SWORD
      amount: 1
    slot: 19
    show: true
    item:
      type: STONE_SWORD
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 75.0
      sellPrice: 15.0

  iron_sword1:
    itemType: ITEM
    display_item:
      type: IRON_SWORD
      amount: 1
    slot: 20
    show: true
    item:
      type: IRON_SWORD
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 250.0
      sellPrice: 50.0

  diamond_sword1:
    itemType: ITEM
    display_item:
      type: DIAMOND_SWORD
      amount: 1
    slot: 21
    show: true
    item:
      type: DIAMOND_SWORD
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 1500.0
      sellPrice: 300.0

  netherite_sword1:
    itemType: ITEM
    display_item:
      type: NETHERITE_SWORD
      amount: 1
      display_name: '&6&lNetherite Sword'
    slot: 22
    show: true
    item:
      type: NETHERITE_SWORD
      amount: 1
    shop:
      ecoType: VAULT
      buyPrice: 10000.0
      sellPrice: 2000.0

  # Special enchanted weapon
  flame_blade:
    itemType: ITEM
    display_item:
      type: DIAMOND_SWORD
      amount: 1
      display_name: '&c&lFlame Blade'
      lore:
        - '&7A sword wreathed in fire'
        - ''
        - '&6Enchantments:'
        - '&7• Sharpness V'
        - '&7• Fire Aspect II'
        - '&7• Unbreaking III'
    slot: 31
    show: true
    item:
      type: DIAMOND_SWORD
      amount: 1
      display_name: '&c&lFlame Blade'
      lore:
        - '&7A sword wreathed in fire'
      enchants:
        1:
          enchant: SHARPNESS
          level: 5
        2:
          enchant: FIRE_ASPECT
          level: 2
        3:
          enchant: UNBREAKING
          level: 3
    shop:
      ecoType: VAULT
      buyPrice: 25000.0
      sellPrice: null
```

---

## Tips

1. **Unique item keys** - Each item needs a unique key (add numbers: `sword1`, `sword2`)
2. **Always set `show: true`** - Items won't appear without this
3. **Use `itemType`** - Required for all items
4. **camelCase for prices** - `buyPrice` not `buy_price`
5. **Wrap prices in `shop:`** - Economy settings go in the shop section
6. **Test changes** - Use `/ishop reload` after editing
