# 🛍️ Shop Files

Configuration reference for individual shop definition files.

---

## File Location

```
plugins/InfiniteShops/shops/
```

Each shop has its own YAML file in this directory.

---

## Basic Structure

```yaml
# shops/example_shop.yml

# Shop metadata
name: 'Example Shop'
permission: ''  # Optional permission to access

# GUI settings
gui:
  title: '&6&l✦ Example Shop ✦'
  rows: 6
  
# Categories in this shop
categories:
  tools:
    name: '&eTools'
    icon:
      material: DIAMOND_PICKAXE
      name: '&e⛏ Tools'
    slot: 10
    
  weapons:
    name: '&cWeapons'
    icon:
      material: DIAMOND_SWORD
      name: '&c⚔ Weapons'
    slot: 12
```

---

## Item Configuration

```yaml
items:
  diamond_pickaxe:
    material: DIAMOND_PICKAXE
    buy_price: 1000
    sell_price: 500
    ecoType: VAULT
    slot: 0
    
  # Custom named item
  legendary_sword:
    material: NETHERITE_SWORD
    name: '&6&lLegendary Blade'
    lore:
      - '&7A weapon of immense power'
      - ''
      - '&eDamage: &c+15'
    enchantments:
      SHARPNESS: 5
      UNBREAKING: 3
    buy_price: 50000
    sell_price: 0  # Cannot sell
    ecoType: VAULT
    slot: 1
```

---

## Multi-Page Shops

```yaml
# Define multiple pages
pages:
  1:
    items:
      # Page 1 items
      diamond_pickaxe:
        slot: 0
        # ...
  2:
    items:
      # Page 2 items
      netherite_pickaxe:
        slot: 0
        # ...

# Navigation buttons
navigation:
  next_page:
    material: ARROW
    name: '&aNext Page →'
    slot: 53
  prev_page:
    material: ARROW
    name: '&c← Previous Page'
    slot: 45
```

---

## Economy Types

Each item can use different economy types:

| Type | Description |
|------|-------------|
| `VAULT` | Standard Vault economy |
| `EXP` | Experience points/levels |
| `ITEM` | Item-based currency |
| `CUSTOM` | Custom currency system |
| `PLAYERPOINTS` | PlayerPoints integration |
| `TOKENENCHANT` | TokenEnchant integration |

```yaml
# Example with different economies
items:
  basic_sword:
    ecoType: VAULT
    buy_price: 100
    
  enchanted_book:
    ecoType: EXP
    buy_price: 30
    exp_type: levels  # or 'points'
    
  rare_item:
    ecoType: ITEM
    item_currency: DIAMOND
    buy_price: 5  # 5 diamonds
```

---

## Actions

```yaml
items:
  command_item:
    material: PAPER
    name: '&aRank Upgrade'
    action: COMMAND
    commands:
      - 'lp user %player% parent set vip'
      - 'msg %player% Rank upgraded!'
    buy_price: 10000
```

---

## Stock Limits

```yaml
items:
  limited_item:
    material: BEACON
    buy_price: 100000
    stock:
      enabled: true
      amount: 10
      global: true  # Shared across all players
      reset: daily  # daily, weekly, never
```

---

## See Also

- [Shop System](../features/shops.md) - Main shop features
- [Currencies](../economy/currencies.md) - Economy types explained
- [Commands](../commands-permissions/commands.md) - Shop commands

---

## Tips

1. **Use descriptive file names** - `tools.yml`, `blocks.yml` for easy management
2. **Organize by category** - Group related items together
3. **Balance buy/sell prices** - Sell price should be 40-60% of buy price
4. **Test after changes** - Always use `/ishop reload` and verify
5. **Use the editor** - In-game editor reduces YAML syntax errors
