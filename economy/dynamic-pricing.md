# 📊 Dynamic Pricing

Automatic price adjustments based on supply and demand!

---

## Overview

Dynamic Pricing automatically adjusts item prices based on how frequently they're bought or sold. This creates a realistic economy where popular items become more expensive and oversupplied items become cheaper.

<!-- 📸 IMAGE PLACEHOLDER: Graph showing price fluctuation over time based on transactions. Dimensions: 700x400px -->

---

## How It Works

### Buy Demand

When players **buy** an item frequently:
- Price **increases**
- Simulates scarcity

### Sell Supply

When players **sell** an item frequently:
- Price **decreases**
- Simulates oversupply

---

## Configuration

```yaml
# In config.yml

features:
  dynamic-pricing: true

dynamic_pricing:
  # Enable the system
  enabled: true
  
  # Price adjustment settings
  buy:
    # Price increase per purchase (%)
    increase_per_purchase: 0.5
    # Maximum price multiplier
    max_multiplier: 2.0
  
  sell:
    # Price decrease per sale (%)
    decrease_per_sale: 0.5
    # Minimum price multiplier
    min_multiplier: 0.5
  
  # Price reset settings
  reset:
    # Enable automatic price reset
    enabled: true
    # Reset interval (seconds)
    interval: 86400  # 24 hours
    # Reset to base price or partial reset
    type: PARTIAL  # FULL or PARTIAL
    # Partial reset amount (%)
    partial_amount: 25
  
  # Notification
  show_price_change: true
```

---

## Price Calculations

### Buy Price Formula

```
Current Buy Price = Base Price × (1 + (purchases × increase_rate))
```

Capped at: `Base Price × max_multiplier`

### Sell Price Formula

```
Current Sell Price = Base Price × (1 - (sales × decrease_rate))
```

Floored at: `Base Price × min_multiplier`

---

## Per-Item Configuration

Configure dynamic pricing per item:

```yaml
# In shop configuration
items:
  diamond:
    material: DIAMOND
    base_buy_price: 100
    base_sell_price: 50
    
    dynamic_pricing:
      enabled: true
      buy_increase: 1%
      buy_max: 3.0  # Up to 300% of base
      sell_decrease: 0.5%
      sell_min: 0.25  # Down to 25% of base
```

---

## Price Display

Show current prices vs base prices:

```yaml
# Item lore configuration
lore:
  - '&7Base Price: &f$%base_price%'
  - '&7Current Price: &a$%current_price%'
  - '&7Market Trend: %trend%'  # ↑ or ↓
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of shop item showing base price, current price, and trend arrow. Dimensions: 400x250px -->

---

## Price Reset Options

### Full Reset

Prices return to base values:

```yaml
reset:
  type: FULL
  interval: 86400  # Daily
```

### Partial Reset

Prices move toward base values:

```yaml
reset:
  type: PARTIAL
  partial_amount: 25  # 25% toward base
  interval: 3600  # Hourly
```

### Manual Reset

```
/ishop dynamicpricing reset [item]
```

---

## Seasonal Integration

With RealisticSeasons plugin, prices can vary by season:

```yaml
dynamic_pricing:
  seasons:
    enabled: true
    modifiers:
      SPRING:
        crops: 0.8  # 20% cheaper crops
      SUMMER:
        crops: 0.7  # 30% cheaper crops
      FALL:
        crops: 1.2  # 20% more expensive
      WINTER:
        crops: 1.5  # 50% more expensive
```

---

## Commands

| Command | Description |
|---------|-------------|
| `/ishop dynamicpricing info <item>` | View item's price history |
| `/ishop dynamicpricing reset [item]` | Reset prices |
| `/ishop dynamicpricing status` | View system status |

---

## PlaceholderAPI

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_price_<item>_buy%` | Current buy price |
| `%infiniteshops_price_<item>_sell%` | Current sell price |
| `%infiniteshops_price_<item>_trend%` | Price trend (↑/↓/→) |
| `%infiniteshops_price_<item>_change%` | Price change % |

---

## Tips

1. **Start with small rates** (0.1-0.5%)
2. **Set reasonable limits** to prevent exploitation
3. **Use partial resets** for smoother economy
4. **Monitor popular items** closely
5. **Combine with taxes** for economy balance
