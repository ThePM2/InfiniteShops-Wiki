# 🌙 Black Market

A thrilling auction-based shop that appears during special events!

---

## Overview

The Black Market is a timed event system where players can bid on exclusive items. It creates excitement and engagement through competitive bidding and limited-time availability.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of the Black Market GUI showing an auction in progress with current bid, time remaining, and item display. Dimensions: 800x500px -->

---

## How It Works

1. **Event Starts** - The Black Market opens (manually or automatically)
2. **Items Rotate** - Exclusive items appear one at a time
3. **Players Bid** - Compete for items by placing bids
4. **Auction Ends** - Highest bidder wins the item
5. **Event Ends** - All items have been auctioned

<!-- 📸 GIF PLACEHOLDER: Animation showing the complete auction flow - bidding, countdown, and winning. Dimensions: 700x450px -->

---

## Configuration

### Main Settings

Edit `plugins/InfiniteShops/blackmarket/config.yml`:

```yaml
# Black Market Configuration

# Enable/disable the feature
enabled: true

# Automatic opening settings
auto_open:
  enabled: true
  # Open on full moon nights (Minecraft time)
  full_moon: true
  # Or use scheduled times
  schedule:
    enabled: false
    times:
      - "20:00"  # 8 PM daily
      - "SATURDAY-14:00"  # Saturday 2 PM

# Event duration settings
duration:
  # Time per item (seconds)
  item_duration: 60
  # Countdown warning times
  warnings: [30, 10, 5, 3, 2, 1]

# Bidding settings
bidding:
  # Minimum starting bid
  min_bid: 100
  # Minimum bid increment
  min_increment: 10
  # Maximum bid (0 = unlimited)
  max_bid: 0
  
# Broadcast settings
broadcast:
  enabled: true
  # Announce new items
  new_item: true
  # Announce bids
  bids: true
  # Announce winners
  winners: true
```

### Adding Items

Create item files in `plugins/InfiniteShops/blackmarket/items/`:

```yaml
# items/legendary_sword.yml

# Item configuration
item:
  material: NETHERITE_SWORD
  name: '&6&l⚔ Legendary Blade'
  lore:
    - '&7A sword of immense power'
    - ''
    - '&eDamage: &c+15'
    - '&eRarity: &6LEGENDARY'
  enchantments:
    SHARPNESS: 10
    UNBREAKING: 5
    FIRE_ASPECT: 2

# Auction settings
auction:
  starting_bid: 50000
  min_increment: 1000
  
# Rarity affects appearance frequency
rarity: LEGENDARY

# Weight for random selection (higher = more common)
weight: 1
```

---

## Admin Commands

| Command | Description |
|---------|-------------|
| `/blackmarket` | Open the Black Market menu |
| `/blackmarket start` | Force start an event |
| `/blackmarket stop` | Force stop the current event |
| `/blackmarket reload` | Reload configuration |
| `/blackmarket status` | View current event status |
| `/blackmarket toggle <setting>` | Toggle settings |

### Status Information

```
/blackmarket status
```

Output:
```
Black Market Status:
- Event: Active
- Current Item: #3/10
- Time Left: 45s
- Current Bid: $15,000
- Total Bids: 23
- Unique Bidders: 8
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of the /blackmarket status command output in chat. Dimensions: 500x200px -->

---

## Bidding System

### How to Bid

1. Open the Black Market: `/blackmarket` or `/bm`
2. View the current item
3. Click to place your bid
4. Enter your bid amount

### Bid Rules

- Bids must be higher than current bid + minimum increment
- Players are notified when outbid
- Winners receive items automatically
- If inventory is full, items are dropped

```yaml
# Outbid notification
BLACK_MARKET_OUTBID: "&6&l[BLACK MARKET] &e%player% &fhas outbid you with &a$%amount%&f!"

# Winning notification  
BLACK_MARKET_WIN: "&6&l[BLACK MARKET] &e&lCongratulations! &fYou won &a%item% &ffor &e$%amount%&f!"
```

---

## Full Moon Trigger

Configure the Black Market to open during full moons:

```yaml
auto_open:
  full_moon: true
  # Additional settings for full moon events
  full_moon_settings:
    # Announce in advance
    pre_announce: 300  # 5 minutes before
    # Special items for full moon only
    full_moon_only_items: true
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing the full moon in Minecraft with Black Market announcement in chat. Dimensions: 600x400px -->

---

## Rarity System

Items have different rarities affecting their appearance:

| Rarity | Color | Appearance Rate |
|--------|-------|-----------------|
| COMMON | &7 (Gray) | Very frequent |
| UNCOMMON | &a (Green) | Frequent |
| RARE | &b (Aqua) | Occasional |
| EPIC | &5 (Purple) | Rare |
| LEGENDARY | &6 (Gold) | Very rare |

```yaml
# Rarity weights for random selection
rarity_weights:
  COMMON: 40
  UNCOMMON: 30
  RARE: 20
  EPIC: 8
  LEGENDARY: 2
```

---

## Purchase Limits

Prevent players from dominating the Black Market:

```yaml
limits:
  # Max items per player per event
  per_event: 3
  # Max items per player per day
  per_day: 5
  # Cooldown between purchases (seconds)
  cooldown: 60
```

---

## GUI Customization

Customize the Black Market interface:

```yaml
gui:
  title: '&8&l☠ &4&lBlack Market &8&l☠'
  rows: 6
  
  # Item display slot
  item_slot: 22
  
  # Bid button
  bid_button:
    slot: 40
    material: GOLD_INGOT
    name: '&e&lPlace Bid'
    lore:
      - '&7Current Bid: &a$%current_bid%'
      - '&7Minimum: &e$%min_bid%'
      - ''
      - '&eClick to bid!'
  
  # Info display
  info:
    slot: 4
    material: CLOCK
    name: '&c&lTime Remaining'
    lore:
      - '&7%time% seconds'
      - ''
      - '&7Item: &f%item_number%/%total_items%'
```

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.blackmarket.use` | Access Black Market | true |
| `infiniteshops.blackmarket.bid` | Place bids | true |
| `infiniteshops.blackmarket.admin` | Admin commands | op |

---

## PlaceholderAPI

Available placeholders for Black Market:

| Placeholder | Description |
|-------------|-------------|
| `%infiniteshops_blackmarket_active%` | Is event active (true/false) |
| `%infiniteshops_blackmarket_timeleft%` | Time remaining |
| `%infiniteshops_blackmarket_currentbid%` | Current highest bid |
| `%infiniteshops_blackmarket_item%` | Current item name |

---

## Tips

1. **Create exclusive items** - Make Black Market items special
2. **Vary event times** - Keep players guessing
3. **Balance starting bids** - Not too high, not too low
4. **Use broadcasts** - Build excitement
5. **Limit purchases** - Give everyone a chance
