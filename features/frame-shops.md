# 🖼️ Frame Shops

Display items in item frames with hologram support!

---

## Overview

Frame Shops use item frames to display shop items in the world. Combined with holograms, they create visually appealing shop displays where players can see exactly what they're buying.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a row of frame shops on a wall with glowing item frames and hologram prices. Dimensions: 800x400px -->

---

## Types of Frame Shops

### Admin Frame Shops

Created by admins, linked to shop categories:
- Infinite stock
- Server-controlled prices
- Perfect for spawn shops

### Player Frame Shops

Created by players with their own items:
- Limited stock (player's inventory)
- Player-set prices
- Great for player markets

---

## Creating Admin Frame Shops

### Step 1: Craft a Shop Item Frame

```yaml
# Recipe in config.yml
frame_shop:
  recipe:
    enabled: true
    shape:
      - 'DSD'
      - 'S S'
      - 'DSD'
    replacer:
      D: DIAMOND
      S: STICK
    result:
      material: ITEM_FRAME  # or GLOW_ITEM_FRAME
      name: '&fShop Item Frame'
      lore:
        - ''
        - '&fPlace this frame on a wall!'
        - ''
      amount: 4
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of crafting recipe for shop item frame in a crafting table. Dimensions: 400x300px -->

### Step 2: Place the Frame

Place the shop item frame on a wall.

### Step 3: Configure with Commands

```
/ishop frame
```

This opens the frame configuration menu:

<!-- 📸 GIF PLACEHOLDER: Animation showing the frame shop configuration GUI - setting item, price, and ecoType. Dimensions: 600x400px -->

### Alternative: Direct Setup

```
/ishop frame set item
/ishop frame set buyPrice 100
/ishop frame set sellPrice 50
/ishop frame set ecoType VAULT
```

---

## Creating Player Frame Shops

### Enable Player Frame Shops

```yaml
# In config.yml
features:
  player-frame-shop: true
```

### Create a Shop

1. Player places a shop item frame
2. Right-clicks with item to set display
3. Configures prices through GUI

### Player Frame Shop Settings

```yaml
player_item_frame_shop:
  # Hologram display
  shop_hologram:
    - ''
    - '&a%sell%: &f%sellPrice%%ecoType%'
    - '&c%buy%: &f%buyPrice%%ecoType%'
    - ''
    - '%actions%'
    - ''
  
  actions: '&e%action% &f%description%'
```

---

## Click Actions

Configure interactions:

```yaml
player_shop_actions:
  LEFT:
    action: BUY
    identifier: 'Left click:'
    description: 'Buy %amount% for %price%'
  RIGHT:
    action: SELL
    identifier: 'Right click:'
    description: 'Sell %amount% for %price%'
```

---

## Hologram Display

Frame shops automatically display holograms with:

- Item name
- Buy price
- Sell price
- Available actions

### Hologram Configuration

```yaml
frame_shop:
  hologram:
    enabled: true
    height_offset: 1.5
    
    # Admin frame shop display
    admin:
      - '&b%material%'
      - '&aBuy: &f%buyPrice%%ecoType%'
      - '&cSell: &f%sellPrice%%ecoType%'
    
    # Player frame shop display
    player:
      - '&e%owner%&7''s Shop'
      - '&b%material%'
      - '&aBuy: &f%buyPrice%%ecoType%'
      - '&cSell: &f%sellPrice%%ecoType%'
```

<!-- 📸 IMAGE PLACEHOLDER: Close-up of a frame shop with visible hologram showing all price information. Dimensions: 500x400px -->

---

## Container Linking

Link frame shops to containers for stock:

### Setting Container Location

```
/ishop frame container
```

Then right-click a chest/barrel to link.

### Stock Behavior

- **Admin Shops**: Unlimited stock
- **Player Shops**: Stock from linked container

---

## Frame Shop Commands

| Command | Description |
|---------|-------------|
| `/ishop frame` | Open frame configuration |
| `/ishop frame set item` | Set display item |
| `/ishop frame set buyPrice <price>` | Set buy price |
| `/ishop frame set sellPrice <price>` | Set sell price |
| `/ishop frame set ecoType <type>` | Set economy type |
| `/ishop frame container` | Link to container |
| `/ishop frame remove` | Remove frame shop |
| `/ishop frame change` | Change display item |

---

## Economy Options

Frame shops support all economy types:

| EcoType | Example |
|---------|---------|
| VAULT | $100 |
| EXP | 30 levels |
| ITEM | 10 diamonds |
| CUSTOM | 500 gems |

---

## Popup GUI

Enable a popup GUI when players approach frame shops:

```yaml
shop_item_frame:
  popup_gui: true
  popup_distance: 3  # blocks
  popup_duration: 5  # seconds
```

<!-- 📸 GIF PLACEHOLDER: Animation showing a popup GUI appearing when player approaches a frame shop. Dimensions: 600x350px -->

---

## Glow Item Frames

Use glowing item frames for better visibility (1.17+):

```yaml
frame_shop:
  recipe:
    result:
      material: GLOW_ITEM_FRAME
```

Items in glow frames emit light, making them visible in dark areas.

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.frame` | Create admin frame shops | op |
| `infiniteshops.frame.player` | Create player frame shops | true |
| `infiniteshops.frame.remove` | Remove frame shops | op |

---

## Configuration Reference

```yaml
# Full frame shop configuration

frame_shop:
  enabled: true
  
  # Recipe for shop item frames
  recipe:
    enabled: true
    shape:
      - 'DSD'
      - 'S S'
      - 'DSD'
    replacer:
      D: DIAMOND
      S: STICK
    result:
      material: GLOW_ITEM_FRAME
      name: '&fShop Item Frame'
      lore:
        - ''
        - '&fPlace on a wall to create a shop!'
        - ''
      amount: 4
  
  # Hologram settings
  hologram:
    enabled: true
    height_offset: 1.5
  
  # Popup GUI
  popup_gui: true
  popup_distance: 3
```

---

## Tips

1. **Use glow frames** for visibility
2. **Position at eye level** for easy access
3. **Group similar items** together
4. **Add clear pricing** in holograms
5. **Link containers** for player shops
