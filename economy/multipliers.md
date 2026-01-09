# 📈 Multipliers

Give players bonus rates on buying and selling!

---

## Overview

Multipliers allow you to give players boosted sell prices or discounted buy prices. Perfect for VIP perks, special events, or promotional periods.

---

## How Multipliers Work

| Type | Effect | Example |
|------|--------|---------|
| **Sell Multiplier** | Increases sell prices | 1.5x = 50% more money when selling |
| **Buy Multiplier** | Decreases buy prices | 1.5x = 33% cheaper purchases |

<!-- 📸 IMAGE PLACEHOLDER: Diagram showing how multipliers affect buy/sell prices with before/after examples. Dimensions: 700x300px -->

---

## Giving Multipliers

### Command Syntax

```
/ishop multiplier add <type> <value> <player> [time]
```

### Types

| Type | Description |
|------|-------------|
| `all` | Both buy and sell |
| `buy` | Buy multiplier only |
| `sell` | Sell multiplier only |

### Examples

```bash
# Give 2x all multiplier for 1 hour
/ishop multiplier add all 2.0 Steve 3600

# Give permanent 1.5x sell multiplier
/ishop multiplier add sell 1.5 Steve

# Give 1.25x buy discount for 30 minutes
/ishop multiplier add buy 1.25 Steve 1800
```

---

## Removing Multipliers

```bash
# Remove all multipliers
/ishop multiplier remove all Steve

# Remove buy multiplier only
/ishop multiplier remove buy Steve

# Remove sell multiplier only
/ishop multiplier remove sell Steve
```

---

## Configuration

### Default Settings

```yaml
# In config.yml

# Default multiplier duration (seconds)
default_multiplier_time: 600  # 10 minutes
```

### Multiplier Priority

If a player already has a multiplier, the higher one takes priority:

```
Player has: 1.5x sell multiplier
Admin gives: 1.25x sell multiplier
Result: Player keeps 1.5x (higher value)
```

---

## Permission-Based Multipliers

Give multipliers automatically based on permissions:

```yaml
# In config.yml
multipliers:
  permission_based:
    enabled: true
    groups:
      vip:
        permission: 'infiniteshops.multiplier.vip'
        sell: 1.1
        buy: 1.1
      vip_plus:
        permission: 'infiniteshops.multiplier.vipplus'
        sell: 1.25
        buy: 1.25
      mvp:
        permission: 'infiniteshops.multiplier.mvp'
        sell: 1.5
        buy: 1.5
```

---

## Multiplier Display

### In Lore

Multipliers can be shown in shop item lore:

```yaml
# In shop item configuration
lore:
  - '&7Your sell multiplier: &a%sell_multiplier%x'
  - '&7Your buy multiplier: &a%buy_multiplier%x'
```

### Active Multiplier Messages

```yaml
# In messages.yml
MULTIPLIER_ALL_RECEIVED: "&fYou received a &asell &fand &cbuy &fmultiplier of &6%multiplier%x"
MULTIPLIER_BUY_RECEIVED: "&fYou received a &cbuy &fmultiplier of &6%multiplier%x"
MULTIPLIER_SELL_RECEIVED: "&fYou received a &asell &fmultiplier of &6%multiplier%x"
```

---

## Command Reference

| Command | Description |
|---------|-------------|
| `/ishop multiplier add <type> <value> <player> [time]` | Give multiplier |
| `/ishop multiplier remove <type> <player>` | Remove multiplier |
| `/ishop multiplier info <player>` | View player's multipliers |
| `/ishop multiplier help` | Show help |

---

## PlaceholderAPI

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_multiplier_sell%` | Current sell multiplier |
| `%infiniteshops_multiplier_buy%` | Current buy multiplier |
| `%infiniteshops_multiplier_sell_time%` | Time remaining on sell |
| `%infiniteshops_multiplier_buy_time%` | Time remaining on buy |

---

## Use Cases

### VIP Perks

Give permanent multipliers to donors:

```bash
/ishop multiplier add all 1.5 VIPPlayer
```

### Weekend Events

Use a scheduled task to give everyone multipliers:

```bash
# Give all online players 2x sell for the weekend
/ishop multiplier add sell 2.0 @a 172800
```

### Voting Rewards

Integrate with voting plugins:

```yaml
# In voting plugin config
rewards:
  - 'ishop multiplier add sell 1.25 %player% 3600'
```

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.multipliers` | Manage multipliers | op |

---

## Tips

1. **Stack with permission-based** multipliers for best flexibility
2. **Use timed multipliers** for events
3. **Display active multipliers** to players
4. **Balance carefully** to not break economy
5. **Combine with taxes** for balance
