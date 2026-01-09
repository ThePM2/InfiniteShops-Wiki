# 🏆 Shopper Ranks

Reward loyal customers with ranks and perks!

---

## Overview

The Shopper Rank system tracks player purchase/sale history and rewards them with ranks that provide discounts and perks. The more players shop, the better their rewards!

<!-- 📸 IMAGE PLACEHOLDER: Progression graphic showing rank tiers from Bronze to Diamond with benefits. Dimensions: 800x300px -->

---

## How It Works

1. Players make purchases/sales
2. Transactions are tracked
3. When thresholds are met, players rank up
4. Higher ranks = better discounts

---

## Configuration

Create `plugins/InfiniteShops/shopper_ranks/config.yml`:

```yaml
# Shopper Ranks Configuration

enabled: true

# What counts toward rank progress
tracking:
  count_purchases: true
  count_sales: true
  track_amount_spent: true
  track_amount_earned: true

# Rank definitions
ranks:
  newcomer:
    # Requirements
    required:
      total_transactions: 0
    # Benefits
    discount: 0%
    display: '&7Newcomer'
    prefix: '&7[New]'
    
  bronze:
    required:
      total_transactions: 50
      total_spent: 10000
    discount: 2%
    display: '&6Bronze'
    prefix: '&6[Bronze]'
    
  silver:
    required:
      total_transactions: 200
      total_spent: 50000
    discount: 5%
    display: '&7Silver'
    prefix: '&f[Silver]'
    
  gold:
    required:
      total_transactions: 500
      total_spent: 200000
    discount: 8%
    display: '&eGold'
    prefix: '&e[Gold]'
    
  platinum:
    required:
      total_transactions: 1000
      total_spent: 500000
    discount: 12%
    display: '&bPlatinum'
    prefix: '&b[Platinum]'
    
  diamond:
    required:
      total_transactions: 2500
      total_spent: 1000000
    discount: 15%
    display: '&bDiamond'
    prefix: '&b✦ [Diamond]'
```

---

## Rank Benefits

### Discounts

Each rank provides automatic discounts on purchases:

```yaml
ranks:
  gold:
    discount: 8%  # 8% off all purchases
```

### Commands on Rank Up

Execute commands when players rank up:

```yaml
ranks:
  gold:
    commands:
      - 'broadcast &e%player% &7has achieved &6Gold &7rank!'
      - 'give %player% gold_ingot 10'
```

### Permissions Granted

Grant permissions upon ranking:

```yaml
ranks:
  platinum:
    permissions:
      - 'infiniteshops.vip'
      - 'infiniteshops.preview'
```

---

## Viewing Ranks

### Your Rank

```
/ishop rank
```

Output:
```
===== Your Shopper Rank =====
Current Rank: Gold
Total Transactions: 523
Total Spent: $215,450
Discount: 8%

Next Rank: Platinum
Progress: 523/1000 transactions
           $215,450/$500,000 spent
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of rank info command output in chat. Dimensions: 500x300px -->

### Other Player's Rank

```
/ishop rank <player>
```

---

## Rank Display

### In Chat

Use PlaceholderAPI to display ranks:

```yaml
# EssentialsX chat format
format: '{infiniteshops_rank_prefix} {DISPLAYNAME}: {MESSAGE}'
```

### In Shop Lore

```yaml
# Shop item lore
lore:
  - '&7Your Rank: %infiniteshops_rank%'
  - '&7Your Discount: &a%infiniteshops_rank_discount%%'
```

---

## Leaderboard

### View Top Shoppers

```
/ishop rank top
```

### Configure Leaderboard

```yaml
leaderboard:
  enabled: true
  display_count: 10
  update_interval: 300  # seconds
  
  # What to rank by
  sort_by: TOTAL_SPENT  # or TRANSACTIONS
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of top shoppers leaderboard. Dimensions: 500x400px -->

---

## Commands

| Command | Description |
|---------|-------------|
| `/ishop rank` | View your rank |
| `/ishop rank <player>` | View player's rank |
| `/ishop rank top` | View leaderboard |
| `/ishop rank set <player> <rank>` | Set player's rank (admin) |
| `/ishop rank reset <player>` | Reset player's progress (admin) |

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.rank.self` | View own rank | true |
| `infiniteshops.rank.other` | View others' ranks | true |
| `infiniteshops.rank.admin` | Admin rank commands | op |

---

## PlaceholderAPI

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_rank%` | Current rank name |
| `%infiniteshops_rank_display%` | Formatted rank display |
| `%infiniteshops_rank_prefix%` | Rank prefix |
| `%infiniteshops_rank_discount%` | Rank discount % |
| `%infiniteshops_rank_transactions%` | Total transactions |
| `%infiniteshops_rank_spent%` | Total spent |
| `%infiniteshops_rank_next%` | Next rank name |
| `%infiniteshops_rank_progress%` | Progress to next rank |

---

## Tips

1. **Set achievable thresholds** for early ranks
2. **Make top ranks special** but attainable
3. **Display rank prefixes** in chat
4. **Create a leaderboard** for competition
5. **Award cosmetic perks** alongside discounts
