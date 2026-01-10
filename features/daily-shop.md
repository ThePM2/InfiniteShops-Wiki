# 📅 Daily Shop

A rotating shop with daily and weekly items, rarity tiers, and special features!

---

## Overview

The Daily Shop automatically rotates items on a schedule, creating a dynamic shopping experience. Items are categorized by rarity, and VIP players can receive special discounts and previews.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of the Daily Shop GUI showing daily items, weekly items, and countdown timers. Dimensions: 800x500px -->

---

## Features

- **Daily Rotation** - Items refresh at midnight
- **Weekly Specials** - Premium items that rotate weekly
- **Rarity Tiers** - Common to Legendary items
- **Purchase Limits** - Per-player and global limits
- **Flash Sales** - Random deep discounts
- **Happy Hours** - Scheduled discount periods
- **Wishlist** - Get notified when desired items appear
- **VIP Perks** - Preview upcoming items and bonus discounts

---

## Configuration

Edit `plugins/InfiniteShops/dailyshop/daily-shop.yml`:

```yaml
# Daily Shop Configuration

enabled: true

# Rotation settings
rotation:
  daily:
    time: "00:00"  # Midnight
    item_count: 6
  weekly:
    day: MONDAY
    time: "00:00"
    item_count: 3

# Display settings
display:
  title: '&6&l✦ Daily Shop ✦'
  rows: 6
  
  # Show countdown timers
  show_timers: true
  glow_rare_items: true
  legendary_particles: true
  
  timer_format:
    daily: "HH:mm:ss"
    weekly: "Dd HHh mmm"
```

<!-- 📸 GIF PLACEHOLDER: Animation showing the Daily Shop timer counting down and items refreshing. Dimensions: 600x400px -->

---

## Rarity Distribution

Control how often each rarity appears:

```yaml
rarity_distribution:
  daily:
    COMMON: 40
    UNCOMMON: 30
    RARE: 20
    EPIC: 8
    LEGENDARY: 2
    MYTHIC: 0
    SPECIAL: 0
  weekly:
    COMMON: 20
    UNCOMMON: 25
    RARE: 30
    EPIC: 20
    LEGENDARY: 5
    MYTHIC: 1
    SPECIAL: 0
```

### Rarity Colors

| Rarity | Display Tag | Color |
|--------|-------------|-------|
| COMMON | &7[COMMON] | Gray |
| UNCOMMON | &a[UNCOMMON] | Green |
| RARE | &b[RARE] | Aqua |
| EPIC | &5[EPIC] | Purple |
| LEGENDARY | &6[LEGENDARY] | Gold |
| MYTHIC | &d[MYTHIC] | Light Purple |
| SPECIAL | &c[SPECIAL] | Red |

---

## Adding Items

Create item pools in `plugins/InfiniteShops/dailyshop/items/`:

```yaml
# items/tools.yml

pool_name: "Tools"
items:
  diamond_pickaxe:
    material: DIAMOND_PICKAXE
    rarity: RARE
    base_price: 2500
    enchantments:
      EFFICIENCY: 4
      UNBREAKING: 3
    
  netherite_sword:
    material: NETHERITE_SWORD
    rarity: LEGENDARY
    base_price: 50000
    enchantments:
      SHARPNESS: 5
      FIRE_ASPECT: 2
    limit:
      global: 5
      player: 1
```

---

## Pricing Configuration

```yaml
pricing:
  currency_type: "VAULT"
  
  # Dynamic pricing based on purchases
  dynamic_pricing: false
  price_increase: 5.0  # % increase per purchase
  max_price_multiplier: 2.0
  reset_on_rotation: true
  
  # Price multipliers by rarity
  rarity_multipliers:
    COMMON: 1.0
    UNCOMMON: 1.5
    RARE: 2.0
    EPIC: 3.0
    LEGENDARY: 5.0
```

---

## Purchase Limits

### Global Limits (Server-wide)

```yaml
limits:
  global:
    enabled: false
    by_rarity:
      COMMON: 100
      UNCOMMON: 50
      RARE: 25
      EPIC: 10
      LEGENDARY: 5
```

### Player Limits

```yaml
limits:
  player:
    enabled: true
    daily_by_rarity:
      COMMON: 10
      UNCOMMON: 5
      RARE: 3
      EPIC: 2
      LEGENDARY: 1
    weekly_by_rarity:
      COMMON: 20
      UNCOMMON: 10
      RARE: 5
      EPIC: 3
      LEGENDARY: 1
```

### VIP Multipliers

```yaml
limits:
  multipliers:
    vip:
      enabled: true
      permission: 'infiniteshops.dailyshop.vip'
      multiplier: 1.2
    vip_plus:
      enabled: true
      permission: 'infiniteshops.dailyshop.vip_plus'
      multiplier: 1.5
    mvp:
      enabled: true
      permission: 'infiniteshops.dailyshop.mvp'
      multiplier: 2.0
```

---

## Special Features

### Flash Sales

Random deep discounts on items:

```yaml
features:
  flash_sales:
    enabled: true
    chance_per_item: 0.05  # 5% chance
    min_discount: 20
    max_discount: 50
    show_banner: true
    announce: true
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing a Flash Sale item with discount banner and special effects. Dimensions: 400x300px -->

### Happy Hours

Scheduled discount periods:

```yaml
features:
  happy_hours:
    enabled: true
    times:
      - start: "12:00"
        end: "13:00"
        discount: 15
      - start: "20:00"
        end: "21:00"
        discount: 20
    global: true
    stackable: false  # Don't stack with flash sales
```

### Bundle Deals

```yaml
features:
  bundles:
    enabled: true
    min_items: 3
    bundle_discount: 10  # 10% off when buying 3+ items
```

### First Purchase Bonus

```yaml
features:
  first_purchase:
    enabled: true
    daily_discount: 20
    weekly_discount: 10
    message: "&aFirst purchase discount applied!"
```

---

## Special Events

### Merchant Monday

Extra items available every Monday:

```yaml
special-events:
  merchant-monday:
    enabled: true
    extra-items: 6  # Additional items on Mondays
```

### Flash Friday

Multiple flash sales every Friday:

```yaml
special-events:
  flash-friday:
    enabled: true
    sales-per-day: 3  # Number of flash sales
```

---

## Holiday Events

Automatic discounts during holidays:

```yaml
holiday-events:
  christmas:
    enabled: true
    discount: 0.20  # 20% off
  halloween:
    enabled: true
    discount: 0.15  # 15% off
  easter:
    enabled: false
    discount: 0.10  # 10% off
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of Daily Shop during a holiday event with festive decorations and discount banners. Dimensions: 600x400px -->

---

## Loyalty Rewards

Reward returning customers with progressive discounts:

```yaml
loyalty:
  enabled: true
  max-discount: 0.20  # Maximum 20% discount
  discount-per-level: 0.02  # 2% per loyalty level
```

Players earn loyalty levels based on purchase history.

---

## Wishlist System

Players can add items to their wishlist and get notified when they appear:

```
/dailyshop wishlist add <item>
/dailyshop wishlist remove <item>
/dailyshop wishlist view
```

```yaml
wishlist:
  enabled: true
  max_items: 20
  notify_on_appear: true
  notification: "&d&l♥ WISHLIST ALERT! &fYour wishlisted item &e%item% &fis now available!"
```

<!-- 📸 GIF PLACEHOLDER: Animation showing adding an item to wishlist and receiving notification when it appears. Dimensions: 600x350px -->

---

## Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/dailyshop` | Open Daily Shop | `infiniteshops.dailyshop.use` |
| `/dailyshop help` | Show help | `infiniteshops.dailyshop.use` |
| `/dailyshop stats` | View your statistics | `infiniteshops.dailyshop.use` |
| `/dailyshop history` | View purchase history | `infiniteshops.dailyshop.use` |
| `/dailyshop preview` | Preview upcoming items (VIP) | `infiniteshops.dailyshop.vip` |
| `/dailyshop reload` | Reload configuration | `infiniteshops.dailyshop.admin` |
| `/dailyshop reset <type>` | Force reset items | `infiniteshops.dailyshop.admin` |
| `/dailyshop toggle` | Enable/disable shop | `infiniteshops.dailyshop.admin` |

---

## Player Statistics

Track player purchases:

```
/dailyshop stats
```

Output:
```
===== Your Daily Shop Stats =====
Total Purchases: 47
Total Spent: $125,350
Loyalty Points: 2,350
```

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.dailyshop.use` | Use the Daily Shop | true |
| `infiniteshops.dailyshop.vip` | VIP benefits | false |
| `infiniteshops.dailyshop.bypass.limit` | Bypass purchase limits | false |
| `infiniteshops.dailyshop.admin` | Admin commands | op |

---

## PlaceholderAPI

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_dailyshop_daily_timeleft%` | Time until daily reset |
| `%infiniteshops_dailyshop_weekly_timeleft%` | Time until weekly reset |
| `%infiniteshops_dailyshop_purchases%` | Player's total purchases |
| `%infiniteshops_dailyshop_spent%` | Player's total spent |

---

## Tips

1. **Balance rarity distribution** - Too many legendaries reduces excitement
2. **Use Happy Hours** - Drive traffic during off-peak times
3. **Set reasonable limits** - Prevent economy exploitation
4. **Enable wishlist** - Increases player engagement
5. **Combine with multipliers** - Give VIPs extra value
