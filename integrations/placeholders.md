# 🧩 PlaceholderAPI

Use InfiniteShops placeholders anywhere!

---

## Overview

InfiniteShops provides extensive PlaceholderAPI support, allowing you to display shop data in scoreboards, chat formats, holograms, and more.

---

## Requirements

- [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/)

PlaceholderAPI is automatically detected and hooked.

---

## Player Placeholders

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `%infiniteshops_balance_VAULT%` | Vault balance | `$1,234.56` |
| `%infiniteshops_balance_<currency>%` | Custom currency balance | `500` |
| `%infiniteshops_balance_<currency>_formatted%` | Formatted balance | `1,234` |

---

## Currency Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_symbol_<currency>%` | Currency symbol |
| `%infiniteshops_prefix_<currency>%` | Currency prefix |
| `%infiniteshops_has_currency_<currency>%` | Currency exists (true/false) |

---

## Multiplier Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_multiplier_sell%` | Current sell multiplier |
| `%infiniteshops_multiplier_buy%` | Current buy multiplier |
| `%infiniteshops_multiplier_sell_time%` | Time remaining (sell) |
| `%infiniteshops_multiplier_buy_time%` | Time remaining (buy) |

---

## Shopper Rank Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_rank%` | Current rank name |
| `%infiniteshops_rank_display%` | Formatted rank display |
| `%infiniteshops_rank_prefix%` | Rank prefix |
| `%infiniteshops_rank_discount%` | Rank discount % |
| `%infiniteshops_rank_transactions%` | Total transactions |
| `%infiniteshops_rank_spent%` | Total money spent |
| `%infiniteshops_rank_next%` | Next rank name |
| `%infiniteshops_rank_progress%` | Progress to next rank % |

---

## Black Market Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_blackmarket_active%` | Event active (true/false) |
| `%infiniteshops_blackmarket_timeleft%` | Time remaining |
| `%infiniteshops_blackmarket_currentbid%` | Current highest bid |
| `%infiniteshops_blackmarket_item%` | Current item name |
| `%infiniteshops_blackmarket_totalbids%` | Total bids placed |

---

## Daily Shop Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_dailyshop_daily_timeleft%` | Daily reset countdown |
| `%infiniteshops_dailyshop_weekly_timeleft%` | Weekly reset countdown |
| `%infiniteshops_dailyshop_purchases%` | Player's total purchases |
| `%infiniteshops_dailyshop_spent%` | Player's total spent |

---

## Leaderboard Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_top_<currency>_<pos>_name%` | Player name at position |
| `%infiniteshops_top_<currency>_<pos>_balance%` | Balance at position |
| `%infiniteshops_top_<currency>_<pos>_balance_formatted%` | Formatted balance |
| `%infiniteshops_rank_<currency>%` | Player's leaderboard rank |

**Example**: `%infiniteshops_top_VAULT_1_name%` returns the richest player's name.

---

## Dynamic Pricing Placeholders

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_price_<item>_buy%` | Current buy price |
| `%infiniteshops_price_<item>_sell%` | Current sell price |
| `%infiniteshops_price_<item>_trend%` | Price trend (↑/↓/→) |
| `%infiniteshops_price_<item>_change%` | Price change % |

---

## Usage Examples

### Scoreboard (using Featherboard)

```yaml
lines:
  - '&6&lEconomy'
  - '&7Balance: &a%infiniteshops_balance_VAULT%'
  - '&7Rank: %infiniteshops_rank_display%'
  - '&7Discount: &a%infiniteshops_rank_discount%%'
  - ''
  - '&b&lBlack Market'
  - '&7Active: %infiniteshops_blackmarket_active%'
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a scoreboard showing InfiniteShops placeholders. Dimensions: 300x400px -->

### Chat Format (EssentialsX)

```yaml
format: '%infiniteshops_rank_prefix% {DISPLAYNAME}: {MESSAGE}'
```

### Hologram (DecentHolograms)

```yaml
lines:
  - '&6&lTop Shoppers'
  - '&e1. &f%infiniteshops_top_VAULT_1_name% - &a%infiniteshops_top_VAULT_1_balance_formatted%'
  - '&e2. &f%infiniteshops_top_VAULT_2_name% - &a%infiniteshops_top_VAULT_2_balance_formatted%'
  - '&e3. &f%infiniteshops_top_VAULT_3_name% - &a%infiniteshops_top_VAULT_3_balance_formatted%'
```

### Tab List (TAB Plugin)

```yaml
header:
  - '&6Rank: %infiniteshops_rank_display%'
  - '&aMoney: %infiniteshops_balance_VAULT%'
```

---

## Tips

1. Use **formatted** variants for better display
2. Combine with **other placeholder plugins**
3. Test placeholders with `/papi parse me <placeholder>`
4. Placeholders update in **real-time**
5. Check for typos in **currency names**
