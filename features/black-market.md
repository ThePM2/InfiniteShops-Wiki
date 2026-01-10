# 🌙 Black Market

Create timed auction events with exclusive deals and bidding systems!

---

## Overview

The Black Market is a special shop system that offers limited-time items with optional auction mechanics. Items rotate on a timer, creating urgency and excitement for players.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of the Black Market GUI with timer and exclusive items. Dimensions: 800x500px -->

---

## Configuration Files

The Black Market uses two configuration files:

| File | Purpose |
|------|---------|
| `blackmarket/blackmarket.yml` | Main settings and items |
| `blackmarket/blackmarket-auction.yml` | Auction-specific settings |

---

## Main Configuration

### blackmarket/blackmarket.yml

```yaml
# Black Market Configuration

# Automatically open GUI when event starts
auto_open_gui: true

# Broadcast purchases to server
broadcast_purchases: true

# Skip to next item when current is purchased
skip_on_purchase: false

# How long each item is available (seconds)
item_duration: 30

# Number of items per event
items_per_event: 5

# Auction Mode Settings
auction_mode:
  enabled: false
  starting_price: 1000.0
  bid_increase_percent: 5.0
  bid_reset_time: 5  # seconds
  one_item_per_server: true
  limit_purchases: false

# Messages
messages:
  event_start: "&6&l[BLACK MARKET] &eThe Black Market has opened!"
  event_end: "&6&l[BLACK MARKET] &cThe Black Market has closed."
  no_event: "&cThe Black Market is not open right now."
  already_purchased: "&cYou have already purchased from this Black Market!"
  insufficient_funds: "&cYou don't have enough money for this item!"

# Items Configuration
items:
  special_sword:
    type: ITEM
    price: 5000.0
    weight: 1
    max_stock: 1
    use_auction_price: true
    item:
      material: DIAMOND_SWORD
      amount: 1
      name: "&6&lBlack Market Sword"
      lore:
        - "&7A mysterious sword from the"
        - "&7depths of the black market."
        - ""
        - "&6Special Edition"
      enchants:
        1:
          enchant: SHARPNESS
          level: 5
        2:
          enchant: UNBREAKING
          level: 3

  mystery_command:
    type: COMMAND
    price: 3000.0
    weight: 2
    commands:
      - "give %player% diamond 64"
      - "msg %player% &aYou received a mystery reward!"
    display_item:
      material: ENDER_CHEST
      name: "&d&lMystery Box"
      lore:
        - "&7What could be inside?"
        - "&7Only one way to find out!"

  rare_shop_item:
    type: SHOP_ITEM
    price: 10000.0
    weight: 1
    shop_category: "your_category_id"
    shop_item: "your_item_id"
    display_item:
      material: NETHER_STAR
      name: "&b&lRare Shop Item"
      lore:
        - "&7Normally unavailable item"
        - "&7from the shop!"
```

---

## Item Types

| Type | Description |
|------|-------------|
| `ITEM` | Physical item given to player |
| `COMMAND` | Executes commands on purchase |
| `SHOP_ITEM` | References an item from another shop |

### ITEM Type

```yaml
items:
  legendary_armor:
    type: ITEM
    price: 25000.0
    weight: 1
    max_stock: 1
    use_auction_price: true
    item:
      material: NETHERITE_CHESTPLATE
      amount: 1
      name: "&5&lShadow Armor"
      lore:
        - "&7Forged in darkness"
      enchants:
        1:
          enchant: PROTECTION
          level: 4
        2:
          enchant: UNBREAKING
          level: 3
```

### COMMAND Type

```yaml
items:
  vip_package:
    type: COMMAND
    price: 50000.0
    weight: 1
    commands:
      - "lp user %player% parent set vip"
      - "eco give %player% 10000"
      - "broadcast &6%player% &epurchased a VIP package!"
    display_item:
      material: NETHER_STAR
      name: "&6&lVIP Package"
      lore:
        - "&7Includes:"
        - "&a• VIP Rank"
        - "&a• $10,000 bonus"
```

### SHOP_ITEM Type

```yaml
items:
  shop_exclusive:
    type: SHOP_ITEM
    price: 15000.0
    weight: 2
    shop_category: "tools"
    shop_item: "enchanted_pickaxe1"
    display_item:
      material: DIAMOND_PICKAXE
      name: "&b&lExclusive Tool"
```

---

## Weight System

Weights determine how often items appear:

```yaml
items:
  common_item:
    weight: 5    # More likely to appear
    
  rare_item:
    weight: 1    # Less likely to appear
```

Higher weight = more frequent appearance in the rotation.

---

## Auction Configuration

### blackmarket/blackmarket-auction.yml

```yaml
# Auction Settings
auction:
  enabled: true
  starting_price: 100.0
  minimum_increment: 10.0
  increment_percent: 5.0
  use_percentage_increment: true
  bid_reset_time: 5  # seconds added when bid placed
  minimum_bidders: 2
  require_minimum_bidders: false
  one_item_per_server: true
  limit_wins_per_event: true
  max_wins_per_player: 3
  allow_auto_bid: false
  max_auto_bid_amount: 100000.0

# Anti-Snipe Protection
anti_snipe:
  enabled: true
  threshold_seconds: 10
  extension_seconds: 5

# Reserve Prices (minimum selling price)
reserve_price:
  enabled: false
  items:
    special_sword: 10000.0
    mystery_command: 5000.0
    rare_shop_item: 20000.0

# Bidding Requirements
requirements:
  require_permission: false
  bid_permission: "infiniteshops.blackmarket.bid"
  minimum_balance: 1000.0
  show_bidder_names: true
  anonymous_bidding: false

# Notifications
notifications:
  notify_on_outbid: true
  notify_on_new_bid: false
  sound_on_bid: true
  sound_on_win: true
  bid_sound: "ENTITY_EXPERIENCE_ORB_PICKUP"
  win_sound: "UI_TOAST_CHALLENGE_COMPLETE"

# Visual Effects
visual_effects:
  particles_enabled: true
  firework_on_win: true
  glowing_item_display: true
  animated_timer: true

# Messages
messages:
  bid_success: "&aYou have successfully bid &e$%amount%&a!"
  bid_fail: "&cYour bid of &e$%amount% &cfailed: %reason%"
  outbid: "&c%player% has outbid you with &e$%amount%&c!"
  win: "&a&lCongratulations! You won %item% for &e$%amount%&a!"
  lose: "&cYou did not win this auction. Better luck next time!"
  reserve_not_met: "&cThe reserve price was not met. Item will not be sold."
  minimum_bidders_not_met: "&cMinimum bidders requirement not met."
  auction_start: "&6&lAUCTION: &e%item% &6starting at &e$%price%"
  auction_end: "&6&lAUCTION ENDED: &e%item% &6sold to &e%winner% &6for &e$%amount%"
  last_call: "&c&lLAST CALL! &e%seconds%s remaining!"
  going_once: "&6Going once for &e$%amount%&6..."
  going_twice: "&6Going twice for &e$%amount%&6..."
  sold: "&a&lSOLD! &6to &e%player% &6for &e$%amount%&6!"
```

---

## Commands

| Command | Description |
|---------|-------------|
| `/blackmarket` | Open the Black Market GUI |
| `/blackmarket start` | Start a Black Market event |
| `/blackmarket stop` | End the current event |
| `/blackmarket reload` | Reload configuration |
| `/blackmarket status` | View current event status |
| `/blackmarket toggle <setting>` | Toggle settings |

### Toggle Options

```
/blackmarket toggle auction    - Toggle auction mode
/blackmarket toggle broadcast  - Toggle purchase broadcasts
/blackmarket toggle autoopen   - Toggle auto-open GUI
```

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.blackmarket.use` | Access the Black Market | true |
| `infiniteshops.blackmarket.admin` | Admin commands | op |
| `infiniteshops.blackmarket.bid` | Place bids in auctions | true |
| `infiniteshops.blackmarket.*` | All Black Market permissions | op |

---

## Placeholders

Use these placeholders in messages:

| Placeholder | Description |
|-------------|-------------|
| `%player%` | Player name |
| `%amount%` | Bid/price amount |
| `%item%` | Item name |
| `%winner%` | Auction winner |
| `%price%` | Starting price |
| `%seconds%` | Time remaining |
| `%currentBid%` | Current highest bid |
| `%totalBids%` | Total number of bids |
| `%uniqueBids%` | Number of unique bidders |

---

## Event Flow

### Standard Mode (Non-Auction)

1. Event starts → Items selected from pool based on weights
2. Each item displays for `item_duration` seconds
3. Players can purchase at fixed price
4. If `skip_on_purchase: true`, moves to next item on purchase
5. Event ends after all items shown

### Auction Mode

1. Event starts → First item put up for auction
2. Players bid, each bid extends timer by `bid_reset_time`
3. Anti-snipe adds time if bid in final seconds
4. Highest bidder wins when timer expires
5. Next item begins auction
6. Event ends after all items auctioned

---

## Tips

1. **Balance item weights** - Ensure variety in each event
2. **Set appropriate prices** - Consider server economy
3. **Use anti-snipe** - Prevents last-second sniping in auctions
4. **Limit wins per player** - Gives more players a chance
5. **Broadcast purchases** - Creates FOMO and excitement
6. **Test item configurations** - Verify all items work correctly

---

## Related Features

- [Daily Shop](daily-shop.md) - Another rotating shop system
- [Currencies](../economy/currencies.md) - Economy integration
- [Multipliers](../economy/multipliers.md) - Price modifiers
