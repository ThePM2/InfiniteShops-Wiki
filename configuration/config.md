# ⚙️ config.yml

Main configuration file reference.

---

## File Location

```
plugins/InfiniteShops/config.yml
```

---

## General Settings

```yaml
# Debug mode - enables verbose logging
debug: false

# Hologram plugin override (auto-detected if empty)
hologram-handler: ""
```

---

## Database Configuration

```yaml
database:
  # Database type: SQLite or MySQL
  type: SQLite
  
  # MySQL settings (only if type is MySQL)
  host: localhost
  port: 3306
  database: infiniteshops
  username: root
  password: ""
  
  # Connection pool settings
  pool:
    max_connections: 10
    min_idle: 2
```

---

## Feature Toggles

```yaml
features:
  black-market: true
  daily-shop: true
  custom-currencies: true
  loot: true
  multipliers: true
  sign: true
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

---

## Shop Settings

```yaml
shop:
  # Economy type display symbols
  ecoType_placeholders:
    VAULT: "$"
    EXP: " XP"
    CUSTOM: " pts"
    PLAYERPOINTS: " points"
    TOKENENCHANT: " tokens"
    NOT_ENABLED: ""
```

---

## Sound Effects

```yaml
sounds:
  buy: ENTITY_EXPERIENCE_ORB_PICKUP
  sell: ENTITY_EXPERIENCE_ORB_PICKUP
  sellall: ENTITY_PLAYER_LEVELUP
  error: ENTITY_VILLAGER_NO
  click: UI_BUTTON_CLICK
  wishlist_add: ENTITY_EXPERIENCE_ORB_PICKUP
  wishlist_remove: ENTITY_ITEM_BREAK
  wishlist_alert: ENTITY_PLAYER_LEVELUP
```

---

## Global Shop Buttons

```yaml
buttons:
  showCurrency:
    display_item: CLOCK
    name: '&7You have &6&l%vault_eco_balance_formatted%'
    slot: 'LAST - 2'
    categories:
      testShop: 25
      testShop2: 24
  
  back:
    display_item: BARRIER
    name: '&cBack'
    slot: LAST
    categories: ALL
    action: PLAYER_COMMAND
    value: ishop
    ignore_main: true
  
  search:
    display_item: OAK_SIGN
    name: '&cSearch'
    slot: 'LAST - 1'
    action: SEARCH
    ignore_main: false
```

---

## Multipliers

```yaml
# Default multiplier duration (seconds)
default_multiplier_time: 600
```

---

## Discounts

```yaml
discounts:
  item_discount:
    chance: '%amount% * 0.25'
    discount: '%amount% * 0.05'
  
  stack:
    chance: '%stack% * 0.5'
    discount: '%stack% * 1'
```

---

## Taxes

```yaml
taxes:
  hidden: false
  tax_lore: ' &6*tax: %tax%'
  
  tax:
    over_1k_vault:
      ecoType: VAULT
      value: 1000
      tax: 1%
    over_5k_vault:
      ecoType: VAULT
      value: 5000
      tax: 2%
    over_100_points:
      ecoType: EXP
      value: 100
      type: points
      tax: 1%
    over_10_levels:
      ecoType: EXP
      value: 10
      type: levels
      tax: 1%
```

---

## Click Actions

```yaml
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

---

## Frame Shop Settings

```yaml
frame_shop:
  recipe:
    enabled: true
    shape:
      - 'DSD'
      - 'S S'
      - 'DSD'
    replacer:
      D: DIAMOND
      S: STICK
    result:
      material: ITEM_FRAME
      name: '&fShop Item Frame'
      lore:
        - ''
        - '&fPlace this frame on a wall!'
        - ''
      amount: 4

player_item_frame_shop:
  shop_hologram:
    - ''
    - '&a%sell%: &f%sellPrice%%ecoType%'
    - '&c%buy%: &f%buyPrice%%ecoType%'
    - ''
    - '%actions%'
    - ''
  
  actions: '&e%action% &f%description%'
```

---

## Preview Settings

```yaml
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

## Limited Stock

```yaml
limited_stock:
  increase_stock_on_selling: true
```

---

## Limited Sell

```yaml
limited_sell:
  increase_sell_on_buying: false
```

---

## NPC Settings

```yaml
npc:
  teleport: true
  clicks:
    RIGHT: TELEPORT
    LEFT: DELETE
    ALL: TELEPORT
```

---

## Shopper Ranks

```yaml
shopper_ranks:
  enabled: true
  # See shopper-ranks.yml for rank definitions
```

---

## Tips

1. **Backup before editing**
2. **Use `/ishop reload`** after changes
3. **Validate YAML syntax**
4. **Test on development server**
