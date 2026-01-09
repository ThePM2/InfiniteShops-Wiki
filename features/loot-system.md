# 🎰 Loot System

Create exciting loot crates with animations and rewards!

---

## Overview

The Loot System allows you to create randomized reward crates. Players can purchase or earn crates, then open them for a chance at various rewards with configurable rarity weights.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a loot crate opening animation with items spinning. Dimensions: 800x450px -->

---

## Creating Loot Crates

### Step 1: Create a Loot Configuration

Create a new file in `plugins/InfiniteShops/loot/`:

```yaml
# loot/treasure.yml

# Display settings
name: '&6&l✦ Treasure Crate ✦'
rows: 3

# Animation settings
animation:
  enabled: true
  type: HORIZONTAL  # HORIZONTAL, VERTICAL, RANDOM
  speed: 2  # ticks between item changes
  duration: 60  # total animation ticks
  sounds:
    rolling: BLOCK_NOTE_BLOCK_PLING
    win: ENTITY_PLAYER_LEVELUP

# Rewards
rewards:
  common_reward:
    material: IRON_INGOT
    amount: 16
    weight: 50
    name: '&7Iron Ingots'
    
  uncommon_reward:
    material: GOLD_INGOT
    amount: 8
    weight: 30
    name: '&eGold Ingots'
    
  rare_reward:
    material: DIAMOND
    amount: 4
    weight: 15
    name: '&bDiamonds'
    
  legendary_reward:
    material: NETHERITE_INGOT
    amount: 1
    weight: 5
    name: '&6&lNetherite Ingot!'
```

<!-- 📸 GIF PLACEHOLDER: Animation showing a loot crate opening with horizontal spinning animation. Dimensions: 600x400px -->

---

## Weight System

Weights determine the probability of each reward:

```
Probability = weight / sum(all weights)
```

Example calculation:
- Common: 50 / 100 = 50%
- Uncommon: 30 / 100 = 30%
- Rare: 15 / 100 = 15%
- Legendary: 5 / 100 = 5%

---

## Reward Types

### Item Rewards

```yaml
rewards:
  diamond_sword:
    material: DIAMOND_SWORD
    amount: 1
    weight: 10
    name: '&bDiamond Sword'
    enchantments:
      SHARPNESS: 3
      UNBREAKING: 2
```

### Command Rewards

```yaml
rewards:
  rank_upgrade:
    type: COMMAND
    weight: 5
    name: '&6VIP Upgrade!'
    commands:
      - 'lp user %player% parent add vip'
    broadcast: '&a%player% &7won a &6VIP Upgrade&7!'
```

### Money Rewards

```yaml
rewards:
  cash_prize:
    type: MONEY
    weight: 20
    name: '&a$1,000 Cash!'
    amount: 1000
```

### Multi-Reward (Jackpot)

```yaml
rewards:
  jackpot:
    type: MULTI
    weight: 1
    name: '&d&l★ JACKPOT! ★'
    rewards:
      - material: DIAMOND
        amount: 64
      - type: MONEY
        amount: 10000
      - type: COMMAND
        command: 'broadcast &6%player% &7hit the JACKPOT!'
```

---

## Animation Styles

### Horizontal Spin

```yaml
animation:
  type: HORIZONTAL
  speed: 2
  duration: 60
```

Items scroll horizontally across the GUI.

### Vertical Spin

```yaml
animation:
  type: VERTICAL
  speed: 2
  duration: 60
```

Items scroll vertically.

### Random Flash

```yaml
animation:
  type: RANDOM
  speed: 1
  duration: 80
```

Items appear randomly, slowing down to final reward.

<!-- 📸 GIF PLACEHOLDER: Side-by-side comparison of horizontal and vertical animation styles. Dimensions: 700x300px -->

---

## GUI Layout

```yaml
# Custom GUI layout
rows: 3

menu:
  - 'YYYYYYYYY'
  - 'YRRRRRRRY'
  - 'YYYYYYYYY'

replaces:
  Y: YELLOW_STAINED_GLASS_PANE
  R: null  # Reward display slots

# Reward display slots (for animation)
reward_slots: [10, 11, 12, 13, 14, 15, 16]
winner_slot: 13  # Center slot shows winning item
```

---

## Opening Loot Crates

### From Shop

Add loot crates to your shops:

```yaml
# In shops/crates.yml
items:
  treasure_crate:
    material: CHEST
    display_name: '&6Treasure Crate'
    lore:
      - '&7Open for random rewards!'
      - ''
      - '&eClick to purchase!'
    buy_price: 5000
    ecoType: VAULT
    action: OPEN_LOOT
    value: treasure  # loot file name
```

### From Command

```
/ishop loot open treasure <player>
```

### With Loot Keys

Create key items that open crates:

```yaml
key:
  enabled: true
  material: TRIPWIRE_HOOK
  name: '&6Treasure Key'
  lore:
    - '&7Right-click to open'
    - '&7a Treasure Crate!'
  glow: true
```

---

## Commands

| Command | Description |
|---------|-------------|
| `/ishop loot create <name>` | Create new loot config |
| `/ishop loot open <loot> [player]` | Open a loot crate |
| `/ishop loot give <loot> <player> [amount]` | Give loot keys |
| `/ishop loot preview <loot>` | Preview possible rewards |
| `/ishop loot reload` | Reload loot configurations |

---

## Preview System

Let players see possible rewards before purchasing:

```yaml
preview:
  enabled: true
  show_chances: true  # Show % chance
  
  gui:
    title: '&8Possible Rewards'
    rows: 6
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of loot preview GUI showing all possible rewards with their chances. Dimensions: 600x400px -->

---

## Loot Locations

Create physical loot spawn points in the world:

```yaml
locations:
  spawn_crate:
    world: world
    x: 100
    y: 64
    z: 100
    respawn_time: 3600  # seconds
    hologram:
      enabled: true
      lines:
        - '&6&lTreasure Crate'
        - '&7Click to open!'
```

---

## Configuration Reference

```yaml
# Complete loot configuration example

name: '&6&l✦ Treasure Crate ✦'
rows: 3

# Animation
animation:
  enabled: true
  type: HORIZONTAL
  speed: 2
  duration: 60
  sounds:
    rolling: BLOCK_NOTE_BLOCK_PLING
    win: ENTITY_PLAYER_LEVELUP
    jackpot: UI_TOAST_CHALLENGE_COMPLETE

# Key item
key:
  enabled: true
  material: TRIPWIRE_HOOK
  name: '&6Treasure Key'
  custom_model_data: 1001

# Preview
preview:
  enabled: true
  show_chances: true

# Rewards
rewards:
  iron:
    material: IRON_INGOT
    amount: 16
    weight: 50
    name: '&7Iron Ingots'
    
  gold:
    material: GOLD_INGOT
    amount: 8
    weight: 30
    name: '&eGold Ingots'
    
  diamond:
    material: DIAMOND
    amount: 4
    weight: 15
    name: '&bDiamonds'
    
  legendary:
    material: NETHERITE_INGOT
    amount: 1
    weight: 5
    name: '&6&lNetherite!'
    commands:
      - 'broadcast &a%player% &7found &6Netherite!'
```

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.loot.admin` | Admin loot commands | op |
| `infiniteshops.loot.menu` | Access loot menu | true |
| `infiniteshops.loot.preview` | Preview rewards | true |

---

## Tips

1. **Balance weights carefully** - Make rare items exciting
2. **Use animations** - They build anticipation
3. **Add sound effects** - Enhance the experience
4. **Include multiple tiers** - Give everyone a chance
5. **Broadcast rare wins** - Creates excitement
