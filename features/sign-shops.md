# 🪧 Sign Shops

Classic sign-based shops for quick and accessible trading!

---

## Overview

Sign Shops provide a traditional Minecraft shop experience using signs. Players can interact with signs to buy or sell items without opening a GUI. Perfect for spawn shops, player markets, or quick-access trading posts.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing multiple sign shops on a wall with different items and prices displayed. Dimensions: 800x400px -->

---

## Sign Types

InfiniteShops supports multiple sign types:

| Type | Description | Example Use |
|------|-------------|-------------|
| `BUY` | Purchase items | Selling diamonds to players |
| `SELL` | Sell items for money | Buying cobblestone from players |
| `TRADE` | Exchange items | Trade 10 coal for 1 iron |
| `COMMAND` | Execute commands | Grant permissions or ranks |
| `ENCHANT` | Apply enchantments | Enchanting services |
| `FREE` | Free items | Welcome kits |
| `DISPOSAL` | Dispose of items | Trash bins |

### Player Shop Types

| Type | Description | Example Use |
|------|-------------|-------------|
| `PLAYER_SHOP` | Player-owned buy/sell | Player markets |
| `PLAYER_BUY` | Player selling items | Selling to other players |
| `PLAYER_SELL` | Player buying items | Buying from other players |

---

## Player Shops (Chest Shops)

Allow players to create their own shops attached to chests!

### Creating a Player Shop

1. Place a chest
2. Place a sign on the chest
3. Write the sign format:

```
Chest-Shop
<amount>
s:<sellPrice> b:<buyPrice>
<ecoType>
```

**Example**:
```
Chest-Shop
64
s:50 b:100
VAULT
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a player-owned chest shop with sign showing prices. Dimensions: 500x350px -->

### Player Shop Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.player.shop` | Create chest shops | true |
| `infiniteshops.player.buy` | Create buy-only shops | true |
| `infiniteshops.player.sell` | Create sell-only shops | true |

### How It Works

1. **Seller places chest** with items to sell
2. **Sign displays** owner name and prices
3. **Buyers click sign** to purchase
4. **Money transfers** automatically to seller
5. **Items transfer** from chest to buyer

### Method 1: Using Commands

1. Look at a wall sign
2. Run the setup command:

```
/ishop sign create <type>
```

3. Configure the sign:

```
/ishop sign set material DIAMOND
/ishop sign set buyPrice 100
/ishop sign set ecoType VAULT
```

### Method 2: Direct Placement

Place a sign with specific format:

```
[Shop]
Diamond
Buy: $100
Sell: $50
```

<!-- 📸 GIF PLACEHOLDER: Animation showing the process of creating a sign shop from placing the sign to completion. Dimensions: 600x400px -->

---

## Sign Configuration

### Basic Buy/Sell Sign

```yaml
# Sign shop data (auto-generated)
type: BUY
material: DIAMOND
amount: 1
buyPrice: 100
sellPrice: 50
ecoType: VAULT
```

### Sign with Container

Attach a chest to your sign shop for inventory:

1. Place a sign on a chest/barrel
2. Create the shop:
```
/ishop sign create BUY
```
3. The container's inventory will be used

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing a sign shop attached to a chest with items flowing between them. Dimensions: 500x400px -->

### Command Sign

Execute commands on purchase:

```
/ishop sign create COMMAND
/ishop sign set buyPrice 1000
/ishop sign command add lp user %player% permission set vip.access
/ishop sign set commandExecutor CONSOLE
```

---

## Sign Display

### Display Item

Show a floating item above the sign:

```
/ishop sign set displayItem DIAMOND
```

### Hologram Support

If a hologram plugin is installed, text appears above signs:

```yaml
# In config.yml
sign_shops:
  hologram:
    enabled: true
    lines:
      - '&b%material%'
      - '&aBuy: &f%buyPrice%'
      - '&cSell: &f%sellPrice%'
```

### Item Frame Display

Display items in an item frame attached to the sign:

```yaml
sign_shops:
  item_frame:
    enabled: true
    glow: true  # Glowing item frame (1.17+)
```

---

## Economy Options

### Vault Economy

```
/ishop sign set ecoType VAULT
/ishop sign set buyPrice 100
```

### Experience

```
/ishop sign set ecoType EXP
/ishop sign set buyPrice 30
/ishop sign set level true  # Use levels instead of points
```

### Item Currency

```
/ishop sign set ecoType ITEM
/ishop sign set buyPrice 5
/ishop sign set currencyMaterial EMERALD
```

---

## Admin Commands

| Command | Description |
|---------|-------------|
| `/ishop sign create <type>` | Create a new sign shop |
| `/ishop sign set <option> <value>` | Set sign options |
| `/ishop sign info` | View sign information |
| `/ishop sign remove` | Remove sign shop |
| `/ishop sign command add <cmd>` | Add command to sign |
| `/ishop sign command remove <index>` | Remove command |
| `/ishop sign command list` | List all commands |

### Available Options

| Option | Values | Description |
|--------|--------|-------------|
| `material` | Any material | Item being sold/bought |
| `amount` | Number | Quantity per transaction |
| `buyPrice` | Number | Price to buy |
| `sellPrice` | Number | Price to sell |
| `ecoType` | VAULT/EXP/ITEM/CUSTOM | Currency type |
| `displayItem` | Any material | Item to display |
| `level` | true/false | Use XP levels |
| `commandExecutor` | PLAYER/CONSOLE | Who runs commands |

---

## Disposal Signs

Create trash bins for players:

```
/ishop sign create DISPOSAL
```

Configure disposal inventory:

```yaml
# In config.yml
disposal:
  rows: 3
  title: '&8Disposal'
  confirm_clear: true
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of disposal inventory GUI with items being thrown away. Dimensions: 400x300px -->

---

## Enchantment Signs

Let players enchant items for a price:

```
/ishop sign create ENCHANT
/ishop sign set enchantment SHARPNESS
/ishop sign set enchantmentLevel 5
/ishop sign set buyPrice 5000
/ishop sign set ecoType VAULT
```

When players interact:
1. Holds an enchantable item
2. Clicks the sign
3. Enchantment is applied
4. Payment is deducted

---

## Free Item Signs

Give items for free:

```
/ishop sign create FREE
/ishop sign set material BREAD
/ishop sign set amount 16
```

Configure free shop settings:

```yaml
free_shop:
  rows: 3
  title: '&aFree Items!'
  cooldown: 3600  # 1 hour between claims
```

---

## Sign Shop Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.sign` | Create/manage sign shops | op |
| `infiniteshops.sign.use` | Use sign shops | true |
| `infiniteshops.sign.bypass` | Bypass sign restrictions | op |

---

## Configuration

```yaml
# In config.yml

sign_shops:
  # Enable sign shop feature
  enabled: true
  
  # Sign text format
  format:
    line1: '&8[&aShop&8]'
    line2: '&f%material%'
    line3: '&aBuy: &f%buyPrice%'
    line4: '&cSell: &f%sellPrice%'
  
  # Interaction sounds
  sounds:
    buy: ENTITY_EXPERIENCE_ORB_PICKUP
    sell: ENTITY_EXPERIENCE_ORB_PICKUP
    error: ENTITY_VILLAGER_NO
  
  # Container settings
  container:
    # Allow any container type
    allow_all: true
    # Allowed containers if allow_all is false
    allowed:
      - CHEST
      - BARREL
      - SHULKER_BOX
```

---

## Tips

1. **Use holograms** for better visibility
2. **Attach containers** for automatic restocking
3. **Create disposal bins** to reduce lag from item drops
4. **Group related shops** together
5. **Add command signs** for services like repairs

---

## Troubleshooting

### Sign Not Working

1. Verify you're looking at the sign when running commands
2. Check permissions
3. Ensure the sign type is valid

### Container Not Linking

1. The sign must be directly attached to the container
2. Check container permissions
3. Verify container is not empty (for sell shops)
