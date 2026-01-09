# 💸 Taxes & Discounts

Balance your economy with taxes and reward players with discounts!

---

## Taxes

Taxes are deducted from sell transactions, helping control money flow in your economy.

### How Taxes Work

When a player sells items:
1. Base sell price is calculated
2. Tax percentage is deducted
3. Player receives the net amount

```
Net Amount = Sell Price - (Sell Price × Tax Rate)
```

---

### Tax Configuration

```yaml
# In config.yml

taxes:
  # Show tax in item lore
  hidden: false
  tax_lore: ' &6*tax: %tax%'
  
  # Tax tiers based on transaction value
  tax:
    over_1k_vault:
      ecoType: VAULT
      value: 1000
      tax: 1%
    over_5k_vault:
      ecoType: VAULT
      value: 5000
      tax: 2%
    over_10k_vault:
      ecoType: VAULT
      value: 10000
      tax: 3%
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

### Tax Display

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of shop item lore showing tax information. Dimensions: 400x200px -->

When `hidden: false`, players see tax info in the item lore:
```
Sell Price: $1,000
*tax: 1% ($10)
You receive: $990
```

---

### Progressive Tax Rates

Create tiered tax brackets:

```yaml
taxes:
  tax:
    tier1:
      ecoType: VAULT
      value: 0
      tax: 0%
    tier2:
      ecoType: VAULT
      value: 1000
      tax: 1%
    tier3:
      ecoType: VAULT
      value: 5000
      tax: 2%
    tier4:
      ecoType: VAULT
      value: 10000
      tax: 3%
    tier5:
      ecoType: VAULT
      value: 50000
      tax: 5%
```

---

## Discounts

InfiniteShops offers multiple discount systems to reward players.

### Item Discount

Random chance for discounts based on purchase amount:

```yaml
# In config.yml

discounts:
  item_discount:
    chance: '%amount% * 0.25'  # 25% per item
    discount: '%amount% * 0.05'  # 5% per item
```

**Example**: Buying 10 items = 2.5% chance for 0.5% discount

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing discount being applied in chat message. Dimensions: 500x150px -->

---

### Stack Discount

Discount for buying in bulk (stacks of 64):

```yaml
discounts:
  stack:
    chance: '%stack% * 0.5'  # 50% per stack
    discount: '%stack% * 1'  # 1% per stack
```

**Example**: Buying 5 stacks = 2.5% chance for 5% discount

---

### Shopper Rank Discounts

Give discounts based on player's shopping history:

```yaml
# In shopper_ranks.yml

ranks:
  bronze:
    required_purchases: 100
    discount: 2%
  silver:
    required_purchases: 500
    discount: 5%
  gold:
    required_purchases: 1000
    discount: 10%
  platinum:
    required_purchases: 5000
    discount: 15%
```

See [Shopper Ranks](shopper-ranks.md) for more details.

---

## Discount Messages

Configure discount notification messages:

```yaml
# In messages.yml
DISCOUNT_APPLIED: " &fand got a discount of &6%discount%%"
TAX_PAID: " &fand paid a tax of &6%tax%"
```

---

## Permission-Based Tax Reduction

VIP players can receive tax reductions:

```yaml
taxes:
  reductions:
    enabled: true
    permissions:
      vip:
        permission: 'infiniteshops.tax.vip'
        reduction: 25%  # 25% less tax
      mvp:
        permission: 'infiniteshops.tax.mvp'
        reduction: 50%  # 50% less tax
      admin:
        permission: 'infiniteshops.tax.bypass'
        reduction: 100%  # No tax
```

---

## Tax-Free Items

Exclude specific items from taxes:

```yaml
# In shop item configuration
items:
  essential_food:
    material: BREAD
    sell_price: 10
    tax_exempt: true  # No tax on this item
```

---

## Configuration Reference

### Full Tax Configuration

```yaml
taxes:
  # Enable tax system
  enabled: true
  
  # Show tax in item lore
  hidden: false
  tax_lore: ' &6*tax: %tax%'
  
  # Tax brackets
  tax:
    tier1:
      ecoType: VAULT
      value: 1000
      tax: 1%
    tier2:
      ecoType: VAULT
      value: 5000
      tax: 2%
    tier3:
      ecoType: VAULT
      value: 10000
      tax: 3%
  
  # VIP reductions
  reductions:
    enabled: true
    permissions:
      vip:
        permission: 'infiniteshops.tax.vip'
        reduction: 25%
```

### Full Discount Configuration

```yaml
discounts:
  # Random discount on purchase
  item_discount:
    enabled: true
    chance: '%amount% * 0.25'
    discount: '%amount% * 0.05'
  
  # Bulk purchase discount
  stack:
    enabled: true
    chance: '%stack% * 0.5'
    discount: '%stack% * 1'
  
  # Permission-based flat discounts
  permissions:
    enabled: true
    groups:
      vip:
        permission: 'infiniteshops.discount.vip'
        discount: 5%
      mvp:
        permission: 'infiniteshops.discount.mvp'
        discount: 10%
```

---

## Tips

1. **Balance taxes carefully** - Too high discourages selling
2. **Use progressive rates** - Fair for all player levels
3. **Reward loyal customers** - Use shopper ranks
4. **Combine with multipliers** - Create VIP packages
5. **Display tax info** - Transparency builds trust
