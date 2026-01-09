# 💵 Currencies

InfiniteShops supports multiple currency types for flexible economy systems!

---

## Overview

InfiniteShops can use various economy types for transactions, allowing you to create diverse shop experiences. From standard Vault economy to custom point systems, you have full control over how players pay for items.

---

## Supported Economy Types

| Type | Description | Plugin Required |
|------|-------------|-----------------|
| `VAULT` | Standard server economy | Vault + Economy plugin |
| `EXP` | Experience points/levels | None |
| `ITEM` | Trade items for items | None |
| `CUSTOM` | Custom currency system | None |
| `PLAYERPOINTS` | PlayerPoints currency | PlayerPoints |
| `TOKENENCHANT` | TokenEnchant tokens | TokenEnchant |
| `OR` | Either currency works | None |
| `AND` | Both currencies required | None |

---

## Using Economy Types

### Vault Economy

Standard money economy:

```yaml
items:
  diamond:
    material: DIAMOND
    buy_price: 100
    sell_price: 50
    ecoType: VAULT
```

### Experience Points

Use player experience as currency:

```yaml
items:
  enchanted_book:
    material: ENCHANTED_BOOK
    buy_price: 30
    ecoType: EXP
    level: true  # Use levels instead of points
```

Configuration:
- `level: true` - Uses XP levels
- `level: false` - Uses XP points (default)

### Item Trading

Trade items for items:

```yaml
items:
  beacon:
    material: BEACON
    buy_price: 64
    ecoType: ITEM
    currency_material: NETHER_STAR
```

Players pay with 64 Nether Stars for 1 Beacon.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing item-for-item trade in a shop GUI. Dimensions: 500x300px -->

---

## Custom Currencies

Create your own currency systems!

### Step 1: Create Currency File

Create `plugins/InfiniteShops/currencies/gems.yml`:

```yaml
# Currency identifier
name: gems

# Display settings
display_name: '&dGems'
symbol: '💎'
prefix: '&d'

# Starting balance for new players
starting_balance: 0

# Currency item (optional)
item:
  enabled: true
  material: AMETHYST_SHARD
  name: '&d&lGem'
  lore:
    - '&7A precious gem!'
    - '&7Right-click to deposit'
  custom_model_data: 1001
  
# Allow withdrawing currency to items
withdrawable: true

# Leaderboard
leaderboard:
  enabled: true
  update_interval: 300  # seconds
```

### Step 2: Use in Shops

```yaml
items:
  special_item:
    material: NETHER_STAR
    buy_price: 100
    ecoType: CUSTOM
    currency: gems  # Your currency name
```

---

## Currency Commands

| Command | Description |
|---------|-------------|
| `/ishop currency <name> balance` | Check balance |
| `/ishop currency <name> balance <player>` | Check other's balance |
| `/ishop currency <name> give <player> <amount>` | Give currency |
| `/ishop currency <name> take <player> <amount>` | Take currency |
| `/ishop currency <name> set <player> <amount>` | Set balance |
| `/ishop currency <name> top` | View leaderboard |

---

## Currency Items

Create physical currency items:

### Claiming Currency

When a player right-clicks a currency item, it's deposited into their account.

### Withdrawing Currency

```
/ishop currency gems withdraw 100
```

Creates a currency item worth 100 gems.

<!-- 📸 GIF PLACEHOLDER: Animation showing player right-clicking currency item and balance increasing. Dimensions: 500x300px -->

---

## Combined Currencies

### OR Currency

Player can pay with either currency:

```yaml
items:
  hybrid_item:
    material: DIAMOND_BLOCK
    ecoType: OR
    prices:
      - type: VAULT
        amount: 10000
      - type: CUSTOM
        currency: gems
        amount: 500
```

### AND Currency

Player must pay with BOTH currencies:

```yaml
items:
  premium_item:
    material: NETHERITE_BLOCK
    ecoType: AND
    prices:
      - type: VAULT
        amount: 50000
      - type: ITEM
        material: NETHER_STAR
        amount: 5
```

---

## Display Placeholders

Configure how currencies appear in GUIs:

```yaml
# In config.yml
shop:
  ecoType_placeholders:
    VAULT: "$"
    EXP: " XP"
    CUSTOM: " gems"
    PLAYERPOINTS: " points"
    TOKENENCHANT: " tokens"
    NOT_ENABLED: ""
```

---

## PlaceholderAPI

Available currency placeholders:

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_balance_<currency>%` | Player's balance |
| `%infiniteshops_balance_<currency>_formatted%` | Formatted balance |
| `%infiniteshops_symbol_<currency>%` | Currency symbol |
| `%infiniteshops_prefix_<currency>%` | Currency prefix |
| `%infiniteshops_top_<currency>_<pos>_name%` | Leaderboard name |
| `%infiniteshops_top_<currency>_<pos>_balance%` | Leaderboard balance |
| `%infiniteshops_rank_<currency>%` | Player's rank |
| `%infiniteshops_has_currency_<currency>%` | Currency exists |

---

## Configuration Reference

### Full Currency Configuration

```yaml
# currencies/gems.yml

name: gems
display_name: '&dGems'
symbol: '💎'
prefix: '&d'
starting_balance: 100

# Physical currency item
item:
  enabled: true
  material: AMETHYST_SHARD
  name: '&d&lGem'
  lore:
    - '&7Value: &d1 Gem'
    - ''
    - '&eRight-click to deposit!'
  custom_model_data: 1001
  glow: true

# Withdrawal settings
withdrawable: true
withdraw_item:
  name: '&d&lGem Voucher (%amount%)'
  lore:
    - '&7Contains: &d%amount% Gems'
    - ''
    - '&eRight-click to claim!'

# Leaderboard
leaderboard:
  enabled: true
  update_interval: 300
  display_count: 10

# Database storage
storage:
  type: SQLITE  # or MYSQL
```

---

## Economy Integration

### Vault Integration

InfiniteShops automatically hooks into Vault:

```
[InfiniteShops] Hooked into Vault economy: EssentialsX
```

### PlayerPoints Integration

Automatically detects PlayerPoints:

```
[InfiniteShops] PlayerPoints integration enabled!
```

### TokenEnchant Integration

Automatically detects TokenEnchant:

```
[InfiniteShops] TokenEnchant integration enabled!
```

---

## Tips

1. **Use custom currencies** for special events
2. **Create currency items** for physical drops
3. **Set up leaderboards** for competition
4. **Balance starting amounts** carefully
5. **Use OR currencies** for flexibility
