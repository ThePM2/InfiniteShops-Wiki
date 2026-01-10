# 🎰 Loot System

Create exciting loot crates with animations and rewards!

---

## Overview

The Loot System allows you to create randomized reward crates with different animation styles. Players can purchase or earn crates, then open them for a chance at various rewards with configurable rarity weights.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a loot crate opening animation with items spinning. Dimensions: 800x450px -->

---

## Animation Types

InfiniteShops supports three distinct loot animation types:

| Type | Description |
|------|-------------|
| `RANDOM` | Instant random reward selection (no animation required) |
| `MINESWEEPER` | Minesweeper-style minigame where players click to reveal prizes |
| `SLOT_MACHINE` | Spinning slot machine animation |

---

## Creating Loot Crates

### Basic Configuration

Loot configurations are stored in `plugins/InfiniteShops/loot/`:

```yaml
# loot/loot.yml - Main loot configuration

# Animation type configuration
loot_shop_animation:
  animation_type: RANDOM  # RANDOM, MINESWEEPER, or SLOT_MACHINE
  animation_id: null  # Required for MINESWEEPER and SLOT_MACHINE

# Items that can be won
items:
  common_reward:
    material: IRON_INGOT
    amount: 16
    
  uncommon_reward:
    material: GOLD_INGOT
    amount: 8
    
  rare_reward:
    material: DIAMOND
    amount: 4
    
  legendary_reward:
    material: NETHERITE_INGOT
    amount: 1
```

---

## RANDOM Animation

The simplest animation type - instantly selects a random reward.

```yaml
loot_shop_animation:
  animation_type: RANDOM
  animation_id: null  # Not required for RANDOM
```

---

## SLOT_MACHINE Animation

Creates a spinning slot machine effect. Requires a separate animation configuration file.

### Step 1: Configure Loot to Use Slot Machine

```yaml
# In your loot configuration
loot_shop_animation:
  animation_type: SLOT_MACHINE
  animation_id: my_slot_machine  # References animation file
```

### Step 2: Create Slot Machine Animation

Create a file in `plugins/InfiniteShops/loot/slot/`:

```yaml
# loot/slot/my_slot_machine.yml

id: my_slot_machine
animation_type: SLOT_MACHINE
size: 3  # Rows (3 = 27 slots)
name: '&6&l✦ Slot Machine ✦'
animation_duration: 3  # Seconds

# Define the spinning lines
lines:
  line1: [10, 11, 12, 13, 14, 15, 16]

# Slots where items appear during animation
items_slots: [10, 11, 12, 13, 14, 15, 16]

# Items that spin in the animation
items:
  - material: IRON_INGOT
    amount: 1
  - material: GOLD_INGOT
    amount: 1
  - material: DIAMOND
    amount: 1
  - material: EMERALD
    amount: 1

# Decorative filler items
fillers:
  0:
    material: BLACK_STAINED_GLASS_PANE
    amount: 1
    display_name: ' '
  # Add more slots as needed

# Navigation buttons
buttons:
  spin_button:
    slot: 22
    display_item:
      type: LEVER
      display_name: '&a&lSPIN!'
      lore:
        - '&7Click to spin!'
    action: SPIN

# Sound effects
sound: BLOCK_NOTE_BLOCK_PLING
```

<!-- 📸 GIF PLACEHOLDER: Animation showing slot machine spinning and landing on a reward. Dimensions: 600x400px -->

---

## MINESWEEPER Animation

Creates an interactive minesweeper-style minigame where players click tiles to reveal prizes or bombs.

### Step 1: Configure Loot to Use Minesweeper

```yaml
# In your loot configuration
loot_shop_animation:
  animation_type: MINESWEEPER
  animation_id: my_minesweeper  # References animation file
```

### Step 2: Create Minesweeper Animation

Create a file in `plugins/InfiniteShops/loot/mine/`:

```yaml
# loot/mine/my_minesweeper.yml

id: my_minesweeper
animation_type: MINESWEEPER
size: 6  # Rows (6 = 54 slots)
name: '&c&l💣 Minesweeper 💣'

# Number of bombs and prizes
bomb_amount: '2-7'  # Range format
prize_amount: '1-5'  # Range format

# Bomb item appearance
bomb:
  material: TNT
  amount: 1
  display_name: '&c&l💥 BOOM!'

# Default inventory layout
default_inventory:
  # Slot: Item configuration
  0:
    material: GRAY_STAINED_GLASS_PANE
    display_name: '&7Click to reveal!'

# Buttons
buttons:
  quit_button:
    slot: 49
    display_item:
      type: BARRIER
      display_name: '&c&lQuit Game'
    action: QUIT

# Sound effects
sound: BLOCK_STONE_BUTTON_CLICK_ON
tnt_sound: ENTITY_GENERIC_EXPLODE
```

<!-- 📸 GIF PLACEHOLDER: Animation showing minesweeper gameplay - clicking tiles and revealing prizes. Dimensions: 600x400px -->

---

## Weight System

Weights determine the probability of each reward:

```
Probability = item_weight / sum(all_weights)
```

Example calculation with weights totaling 100:
- Common (weight: 50): 50/100 = 50%
- Uncommon (weight: 30): 30/100 = 30%
- Rare (weight: 15): 15/100 = 15%
- Legendary (weight: 5): 5/100 = 5%

---

## Reward Configuration

### Item Rewards

```yaml
items:
  diamond_sword:
    material: DIAMOND_SWORD
    amount: 1
    display_name: '&bDiamond Sword'
    lore:
      - '&7A powerful weapon'
    enchants:
      1:
        enchant: SHARPNESS
        level: 3
      2:
        enchant: UNBREAKING
        level: 2
```

### Reward with Commands

```yaml
items:
  vip_reward:
    material: NETHER_STAR
    amount: 1
    display_name: '&6VIP Upgrade!'
    commands:
      - 'lp user %player% parent add vip'
      - 'broadcast &a%player% &7won a &6VIP Upgrade!'
```

---

## Opening Loot Crates

### From Shop

Add loot crates to your shops using the COMMAND item type:

```yaml
# In shops/crates.yml
items:
  treasure_crate:
    itemType: COMMAND
    display_item:
      type: CHEST
      amount: 1
      display_name: '&6Treasure Crate'
      lore:
        - '&7Open for random rewards!'
        - ''
        - '&eClick to purchase!'
    slot: 13
    show: true
    shop:
      ecoType: VAULT
      buyPrice: 5000.0
    commands:
      - 'ishop loot open treasure %player%'
```

### From Command

```
/ishop loot open <loot_name> <player>
```

---

## Commands

| Command | Description |
|---------|-------------|
| `/ishop loot create <name>` | Create new loot configuration |
| `/ishop loot open <loot> [player]` | Open a loot crate for a player |
| `/ishop loot reload` | Reload loot configurations |

---

## Loot Actions

Configure what happens when different animation types complete in `loot/loot.yml`:

```yaml
loot_action:
  RANDOM: 'default_action'
  MINESWEEPER: 'minesweeper_action'
  SLOT_MACHINE: 'slot_action'
```

---

## Placeholders

Available placeholders for loot displays:

```yaml
placeholders:
  admin_description: '&7Admin loot configuration'
  # Add custom placeholders as needed
```

---

## Display Items

Configure how each animation type appears in menus:

```yaml
displays:
  default-random:
    material: CHEST
    display_name: '&aRandom Loot'
  default-minesweeper:
    material: TNT
    display_name: '&cMinesweeper'
  default-slot_machine:
    material: LEVER
    display_name: '&6Slot Machine'
```

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.loot.admin` | Admin loot commands | op |
| `infiniteshops.loot.use` | Use loot crates | true |

---

## Tips

1. **Balance weights carefully** - Make rare items exciting but achievable
2. **Use appropriate animations** - SLOT_MACHINE for excitement, RANDOM for quick rewards
3. **Add sound effects** - Enhance the experience with audio feedback
4. **Test bomb ratios** - For MINESWEEPER, ensure fair bomb/prize balance
5. **Broadcast rare wins** - Creates server-wide excitement
