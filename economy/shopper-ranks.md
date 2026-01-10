# 🏆 Shopper Ranks

Reward your most active traders with progression ranks and exclusive benefits!

---

## Overview

The Shopper Ranks system provides a progression path for players based on their trading activity. As players buy and sell items, they earn points and advance through ranks, unlocking multipliers, discounts, and special rewards.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing rank progression UI with benefits. Dimensions: 800x400px -->

---

## Configuration Files

Ranks are configured in individual files in `plugins/InfiniteShops/shopper_ranks/`:

```
shopper_ranks/
├── trade_specialist.yml
├── elite_dealer.yml
├── prestigious_merchant.yml
├── tycoon_of_trade.yml
├── supreme_seller.yml
├── empire_builder.yml
├── magnate_of_merchants.yml
└── legendary_merchant_king.yml
```

---

## Rank Structure

Each rank file follows this format:

```yaml
# shopper_ranks/trade_specialist.yml

# Unique identifier
id: TradeSpecialist

# Display name with %level% placeholder
display_name: '&bTrade Specialist %level%'

# Available levels within this rank
levels: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Next rank after completing all levels (optional)
next_rank: CommerceMaster

# Symbols displayed for each level
symbols:
  1: I
  2: II
  3: III
  4: IV
  5: V
  6: VI
  7: VII
  8: VIII
  9: IX
  10: X

# Points formula (supports %level% placeholder)
required_points: '4750 * %level%'

# Requirements per level
requirements:
  1:
    requirement_type: COLLECT
    amount: 1
    material: EMERALD
  2:
    requirement_type: DROP
    amount: 1
    material: EMERALD
  3:
    requirement_type: BUY_TYPE
    amount: 1
    material: EMERALD
  4:
    requirement_type: GAIN
    amount: 10
  5:
    requirement_type: GAIN
    amount: 10

# Benefits per level
benefits:
  1:
    benefit_type: MULTIPLIER
    value: 1.05
  2:
    benefit_type: MULTIPLIER
    value: 1.075
  3:
    benefit_type: MULTIPLIER
    value: 1.1
  4:
    benefit_type: MULTIPLIER
    value: 1.125
  5:
    benefit_type: MULTIPLIER
    value: 1.15
```

---

## Requirement Types

| Type | Description | Fields |
|------|-------------|--------|
| `SPEND` | Spend X amount of money | `amount` |
| `GAIN` | Earn X amount of money | `amount` |
| `COLLECT` | Collect X of a material | `amount`, `material` |
| `DROP` | Drop/dispose X of a material | `amount`, `material` |
| `BUY_TYPE` | Buy X of a specific material | `amount`, `material` |
| `SELL_TYPE` | Sell X of a specific material | `amount`, `material` |
| `SELL_BUY` | Combined buy/sell transactions | `amount` |

### Requirement Examples

```yaml
requirements:
  # Spend money requirement
  1:
    requirement_type: SPEND
    amount: 15
    
  # Collect specific item
  2:
    requirement_type: COLLECT
    amount: 64
    material: DIAMOND
    
  # Sell specific item
  3:
    requirement_type: SELL_TYPE
    amount: 128
    material: WHEAT
    
  # Buy specific item
  4:
    requirement_type: BUY_TYPE
    amount: 32
    material: IRON_INGOT
    
  # General trading activity
  5:
    requirement_type: SELL_BUY
    amount: 100
```

---

## Benefit Types

| Type | Description | Fields |
|------|-------------|--------|
| `MULTIPLIER` | Multiply sell prices | `value` |
| `DISCOUNT` | Discount on purchases | `value`, `chance` |
| `TAX_REDUCE` | Reduce tax on transactions | `value`, `chance` |
| `RANDOM_ITEM` | Chance for random item reward | `chance`, `items` |

### Benefit Examples

```yaml
benefits:
  # Sell price multiplier (1.05 = 5% more money)
  1:
    benefit_type: MULTIPLIER
    value: 1.05
    
  # Purchase discount (3.5% discount, 2.5% chance)
  2:
    benefit_type: DISCOUNT
    value: 3.5
    chance: 2.5
    
  # Tax reduction (5% reduction, 7.5% chance)
  3:
    benefit_type: TAX_REDUCE
    value: 5
    chance: 7.5
    
  # Random item reward
  4:
    benefit_type: RANDOM_ITEM
    chance: 1
    items:
      1:
        material: DIAMOND_BLOCK
        amount: 1
      2:
        material: NETHERITE_SCRAP
        amount: 2
      3:
        material: ENCHANTED_BOOK
        amount: 1
        enchants:
          1:
            enchant: MENDING
            level: 1
```

---

## Complete Rank Example

```yaml
# shopper_ranks/elite_dealer.yml

id: EliteDealer
display_name: '&dElite Dealer %level%'
levels: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
next_rank: PrestigiousMerchant

symbols:
  1: I
  2: II
  3: III
  4: IV
  5: V
  6: VI
  7: VII
  8: VIII
  9: IX
  10: X

required_points: '5500 * %level%'

requirements:
  1:
    requirement_type: SELL_BUY
    amount: 10
  2:
    requirement_type: SELL_BUY
    amount: 10
  3:
    requirement_type: SELL_BUY
    amount: 10
  4:
    requirement_type: SELL_BUY
    amount: 10
  5:
    requirement_type: SELL_BUY
    amount: 10
  6:
    requirement_type: SELL_TYPE
    material: CACTUS
    amount: 8
  7:
    requirement_type: SELL_TYPE
    material: WHEAT
    amount: 8
  8:
    requirement_type: SELL_TYPE
    material: CARROT
    amount: 8
  9:
    requirement_type: SELL_TYPE
    material: POTATO
    amount: 8
  10:
    requirement_type: SELL_TYPE
    material: COAL
    amount: 8

benefits:
  1:
    benefit_type: RANDOM_ITEM
    chance: 1
    items:
      1:
        material: NETHERITE_SCRAP
        amount: 2
      2:
        material: DIAMOND_BLOCK
        amount: 1
      3:
        material: DIAMOND_PICKAXE
        amount: 1
      4:
        material: ENCHANTED_BOOK
        amount: 1
        enchants:
          1:
            enchant: MENDING
            level: 1
      5:
        material: IRON_BLOCK
        amount: 2
      6:
        material: EMERALD_BLOCK
        amount: 4
  2:
    benefit_type: MULTIPLIER
    value: 1.475
  3:
    benefit_type: MULTIPLIER
    value: 1.5
  4:
    benefit_type: DISCOUNT
    value: 3.5
    chance: 2.5
  5:
    benefit_type: DISCOUNT
    value: 3.5
    chance: 2.75
  6:
    benefit_type: DISCOUNT
    value: 3.5
    chance: 3
  7:
    benefit_type: DISCOUNT
    value: 3.75
    chance: 2.5
  8:
    benefit_type: DISCOUNT
    value: 3.75
    chance: 2.75
  9:
    benefit_type: DISCOUNT
    value: 4
    chance: 2.5
  10:
    benefit_type: DISCOUNT
    value: 5
    chance: 2.5
```

---

## Rank with Special Symbols

```yaml
# shopper_ranks/empire_builder.yml

id: EmpireBuilder
display_name: '&9Empire Builder %level%'
levels: [1, 2, 3, 4, 5]
next_rank: MagnateOfMerchants

# Using emoji symbols
symbols:
  1: 🏦
  2: 🏦🏦
  3: 🏦🏦🏦
  4: 🏦🏦🏦🏦
  5: 🏦🏦🏦🏦🏦

required_points: '7500 * %level%'

requirements:
  1:
    requirement_type: GAIN
    amount: 35
  2:
    requirement_type: GAIN
    amount: 35
  3:
    requirement_type: GAIN
    amount: 40
  4:
    requirement_type: GAIN
    amount: 45
  5:
    requirement_type: GAIN
    amount: 50

benefits:
  1:
    benefit_type: TAX_REDUCE
    value: 5
    chance: 7.5
  2:
    benefit_type: MULTIPLIER
    value: 1.575
  3:
    benefit_type: DISCOUNT
    value: 3.75
    chance: 5
  4:
    benefit_type: MULTIPLIER
    value: 1.6
  5:
    benefit_type: MULTIPLIER
    value: 1.6125
```

---

## Final Rank (No next_rank)

```yaml
# shopper_ranks/legendary_merchant_king.yml

id: LegendaryMerchantKing
display_name: '&4L&ce&fg&ce&4n&cd&fa&cr&4y &cM&fe&cr&4c&ch&fa&cn&4t &cK&fi&cn&4g &6%level%'
levels: [1, 2, 3]
# No next_rank - this is the final rank

symbols:
  1: 👑
  2: 👑👑
  3: 👑👑👑

required_points: '9500 * %level%'

requirements:
  1:
    requirement_type: SPEND
    amount: 55
  2:
    requirement_type: SPEND
    amount: 65
  3:
    requirement_type: SPEND
    amount: 75

benefits:
  1:
    benefit_type: MULTIPLIER
    value: 1.75
  2:
    benefit_type: MULTIPLIER
    value: 1.8
  3:
    benefit_type: MULTIPLIER
    value: 1.85
```

---

## Commands

| Command | Description |
|---------|-------------|
| `/ishop rank info` | View your rank information |
| `/ishop rank info <player>` | View another player's rank |
| `/ishop rank progress` | View progress to next level |

---

## Placeholders

Use these in messages and displays:

| Placeholder | Description |
|-------------|-------------|
| `%player%` | Player name |
| `%current_rank%` | Current rank display name |
| `%next_rank%` | Next rank display name |
| `%progress%` | Progress percentage |
| `%current_points%` | Current points |
| `%required_points%` | Points needed for next level |
| `%requirement%` | Current requirement description |
| `%benefit%` | Current benefit description |
| `%requirement_type%` | Type of requirement |
| `%amount%` | Requirement amount |
| `%material%` | Required material |
| `%benefit_type%` | Type of benefit |
| `%value%` | Benefit value |
| `%chance%` | Benefit chance |

---

## Tips

1. **Create progression** - Early ranks should be easier to achieve
2. **Meaningful benefits** - Higher ranks deserve better rewards
3. **Variety in requirements** - Mix different requirement types
4. **Balance multipliers** - Don't make them too powerful
5. **Use symbols** - Visual progression motivates players
6. **Test the math** - Verify points formulas work correctly

---

## Default Rank Progression

The default InfiniteShops installation includes this rank chain:

1. **Trade Specialist** (10 levels) → 
2. **Elite Dealer** (10 levels) → 
3. **Prestigious Merchant** (5 levels) → 
4. **Tycoon of Trade** (5 levels) → 
5. **Supreme Seller** (5 levels) → 
6. **Empire Builder** (5 levels) → 
7. **Magnate of Merchants** (5 levels) → 
8. **Legendary Merchant King** (3 levels) - Final rank
