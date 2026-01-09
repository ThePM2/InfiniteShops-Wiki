# 💬 Messages

Customizing plugin messages and translations.

---

## File Location

```
plugins/InfiniteShops/messages.yml
```

---

## Overview

All plugin messages can be customized in the messages file. Messages support:

- **Color codes** (`&a`, `&b`, `&c`, etc.)
- **Hex colors** (`&#FF5733`)
- **Placeholders** (`%player%`, `%amount%`, etc.)
- **MiniMessage format** (optional)

---

## General Messages

```yaml
# Prefix for all messages
prefix: '&8[&6InfiniteShops&8] '

# General messages
no_permission: '&cYou do not have permission to do this.'
player_only: '&cThis command can only be run by players.'
invalid_command: '&cInvalid command. Use &e/ishop help &cfor help.'
reload_success: '&aConfiguration reloaded successfully!'
```

---

## Shop Messages

```yaml
shop:
  opened: '&7Opening shop: &e%shop%'
  closed: '&cThis shop is currently closed.'
  no_permission: '&cYou cannot access this shop.'
  
  buy:
    success: '&aYou bought &e%amount%x %item% &afor &e%price%&a!'
    insufficient_funds: '&cYou need &e%price% &cto buy this item.'
    inventory_full: '&cYour inventory is full!'
    
  sell:
    success: '&aYou sold &e%amount%x %item% &afor &e%price%&a!'
    no_items: '&cYou don''t have any of this item to sell.'
    not_sellable: '&cThis item cannot be sold.'
```

---

## Economy Messages

```yaml
economy:
  balance: '&7Your balance: &e%balance%'
  insufficient: '&cInsufficient funds. You need &e%required% &cbut have &e%balance%&c.'
  
  exp:
    insufficient_levels: '&cYou need &e%required% levels &cbut have &e%current%&c.'
    insufficient_points: '&cYou need &e%required% XP points &cbut have &e%current%&c.'
```

---

## Daily Shop Messages

```yaml
daily_shop:
  reset: '&a&l✦ &aThe Daily Shop has reset! New items available!'
  weekly_reset: '&6&l✦ &6Weekly specials have changed!'
  purchased: '&aYou purchased &e%item% &afrom the Daily Shop!'
  limit_reached: '&cYou''ve reached your purchase limit for this item.'
  
  flash_sale:
    start: '&e&l⚡ FLASH SALE! &e%item% &7is now &a%discount%% off&7!'
    end: '&7The flash sale has ended.'
```

---

## Black Market Messages

```yaml
black_market:
  open: '&4&l☠ The Black Market is now open!'
  close: '&7The Black Market has closed.'
  bid_placed: '&aYou placed a bid of &e%amount% &aon &e%item%&a!'
  outbid: '&c%player% &7has outbid you on &e%item% &7with &a%amount%&7!'
  won: '&a&lCongratulations! &aYou won &e%item% &afor &e%amount%&a!'
  auction_start: '&6&l▶ &eNow auctioning: &f%item%'
  countdown: '&c%seconds% &7seconds remaining!'
```

---

## Multiplier Messages

```yaml
multipliers:
  activated: '&a&l✦ &a%type% Multiplier activated! &e%multiplier%x &afor &e%duration%&a!'
  expired: '&7Your %type% multiplier has expired.'
  active: '&7Active multipliers:'
  none: '&7You have no active multipliers.'
```

---

## Shopper Rank Messages

```yaml
shopper_ranks:
  rank_up: '&a&l✦ RANK UP! &aYou are now a &e%rank%&a!'
  points_earned: '&7+%points% loyalty points'
  discount_applied: '&a%discount%% &7rank discount applied!'
```

---

## Placeholder Reference

| Placeholder | Description |
|-------------|-------------|
| `%player%` | Player name |
| `%item%` | Item name |
| `%amount%` | Item amount |
| `%price%` | Price (formatted) |
| `%balance%` | Player balance |
| `%shop%` | Shop name |
| `%discount%` | Discount percentage |
| `%multiplier%` | Multiplier value |
| `%duration%` | Time duration |
| `%rank%` | Shopper rank name |

---

## Color Reference

### Standard Colors
| Code | Color |
|------|-------|
| `&0` | Black |
| `&1` | Dark Blue |
| `&2` | Dark Green |
| `&3` | Dark Aqua |
| `&4` | Dark Red |
| `&5` | Dark Purple |
| `&6` | Gold |
| `&7` | Gray |
| `&8` | Dark Gray |
| `&9` | Blue |
| `&a` | Green |
| `&b` | Aqua |
| `&c` | Red |
| `&d` | Light Purple |
| `&e` | Yellow |
| `&f` | White |

### Formatting
| Code | Format |
|------|--------|
| `&l` | Bold |
| `&o` | Italic |
| `&n` | Underline |
| `&m` | Strikethrough |
| `&k` | Obfuscated |
| `&r` | Reset |

### Hex Colors

Use `&#RRGGBB` format:
```yaml
example: '&#FF5733This is orange text!'
gradient: '&#FF0000R&#FF7F00a&#FFFF00i&#00FF00n&#0000FFb&#4B0082o&#9400D3w'
```

---

## Tips

1. **Use PlaceholderAPI** - Messages support PAPI placeholders
2. **Test colors** - Use `/ishop test-message <message>` to preview
3. **Backup first** - Always backup messages.yml before editing
4. **Escape quotes** - Use `''` for single quotes in YAML strings
