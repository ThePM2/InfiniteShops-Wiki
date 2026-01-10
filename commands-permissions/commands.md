# 📝 Commands

Complete reference for all InfiniteShops commands.

---

## Main Commands

### /shop

Opens the main shop menu or a specific shop.

```bash
/shop              # Open main shop
/shop <category>   # Open specific shop category
/shop search <q>   # Search for items
```

**Aliases**: `/s`, `/shp`

### /infiniteshops

Main admin command hub.

```bash
/infiniteshops          # Show help
/infiniteshops help     # Detailed help
/infiniteshops reload   # Reload all configs
/infiniteshops editor   # Open shop editor
```

**Aliases**: `/ishop`, `/infshops`, `/infshop`, `/infs`

---

## Shop Management

| Command | Description |
|---------|-------------|
| `/ishop reload` | Reload all configuration files |
| `/ishop editor` | Open the in-game shop editor |
| `/ishop create <n>` | Create a new shop category |
| `/ishop delete <n>` | Delete a shop category |
| `/ishop list` | List all shop categories |

<!-- 📸 GIF PLACEHOLDER: Animation showing the in-game shop editor in action. Dimensions: 600x400px -->

---

## Black Market Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/blackmarket` | Open Black Market menu | `infiniteshops.blackmarket.use` |
| `/blackmarket start` | Force start event | `infiniteshops.blackmarket.admin` |
| `/blackmarket stop` | Force stop event | `infiniteshops.blackmarket.admin` |
| `/blackmarket reload` | Reload configuration | `infiniteshops.blackmarket.admin` |
| `/blackmarket status` | View current status | `infiniteshops.blackmarket.admin` |
| `/blackmarket toggle <setting>` | Toggle settings | `infiniteshops.blackmarket.admin` |

### Toggle Options
- `auction` - Toggle auction mode
- `broadcast` - Toggle purchase broadcasts
- `autoopen` - Toggle auto-open GUI

**Aliases**: `/bm`, `/blackm`

---

## Daily Shop Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/dailyshop` | Open Daily Shop | `infiniteshops.dailyshop.use` |
| `/dailyshop help` | Show help menu | `infiniteshops.dailyshop.use` |
| `/dailyshop preview` | Preview upcoming items | `infiniteshops.dailyshop.vip` |
| `/dailyshop reload` | Reload configuration | `infiniteshops.dailyshop.admin` |
| `/dailyshop reset` | Reset shop items | `infiniteshops.dailyshop.admin` |

**Aliases**: `/ds`, `/dshop`

---

## NPC Commands

Requires **Citizens** plugin.

| Command | Description |
|---------|-------------|
| `/ishop npc` | Show NPC help |
| `/ishop npc create <name>` | Create an NPC with name |
| `/ishop npc create <name> -c` | Create NPC centered on block |
| `/ishop npc create <name> -t <type>` | Create NPC with entity type |
| `/ishop npc create <name> -c -t <type>` | Create centered NPC with type |

### NPC Creation Options

| Flag | Description | Example |
|------|-------------|---------|
| `-c` | Center NPC on block | `/ishop npc create Shopkeeper -c` |
| `-t <type>` | Set entity type | `/ishop npc create Guard -t ZOMBIE` |

### Full Syntax
```bash
/ishop npc create <name> -c(center/optional) -t(entity type/optional)
```

### Examples
```bash
# Create a basic NPC named "Merchant"
/ishop npc create Merchant

# Create centered NPC
/ishop npc create Merchant -c

# Create a Villager NPC
/ishop npc create Villager_Shop -t VILLAGER

# Create centered Zombie NPC
/ishop npc create Undead_Trader -c -t ZOMBIE
```

After creating an NPC, use the settings GUI to configure the shop link and appearance.

---

## Sign Shop Commands

| Command | Description |
|---------|-------------|
| `/ishop sign command add <command>` | Add command to sign |
| `/ishop sign command remove <index>` | Remove command by index |
| `/ishop sign command list` | List all commands on sign |
| `/ishop sign info <signType>` | View sign type information |

### Sign Command Syntax
```bash
/ishop sign command add <command>
/ishop sign command remove <command>
/ishop sign command list
/ishop sign info <signType>
```

### Sign Types
Use `/ishop sign info <type>` to learn about each type:

| Type | Description |
|------|-------------|
| `ADMIN_SHOP` | Buy and sell with unlimited stock |
| `ADMIN_SELL` | Sell only with unlimited stock |
| `ADMIN_BUY` | Buy only with unlimited stock |
| `PLAYER_SHOP` | Player-owned buy/sell shop |
| `PLAYER_SELL` | Player-owned sell shop |
| `PLAYER_BUY` | Player-owned buy shop |
| `COMMAND` | Execute commands on click |
| `FREE` | Free item distribution |
| `DISPOSAL` | Item disposal sign |
| `ENCHANT` | Enchantment service |

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

## Loot Commands

| Command | Description |
|---------|-------------|
| `/ishop loot create <n>` | Create new loot config |
| `/ishop loot open <loot> [player]` | Open a loot crate |
| `/ishop loot reload` | Reload loot configurations |

---

## Currency Commands

| Command | Description |
|---------|-------------|
| `/ishop currency <n> balance` | Check your balance |
| `/ishop currency <n> balance <player>` | Check player's balance |
| `/ishop currency <n> give <player> <amount>` | Give currency |
| `/ishop currency <n> take <player> <amount>` | Take currency |
| `/ishop currency <n> set <player> <amount>` | Set balance |

---

## Multiplier Commands

| Command | Description |
|---------|-------------|
| `/ishop multiplier add <type> <value> <player> [time]` | Give multiplier |
| `/ishop multiplier remove <type> <player>` | Remove multiplier |
| `/ishop multiplier info <player>` | View player's multipliers |
| `/ishop multiplier help` | Show help |

**Types**: `all`, `buy`, `sell`

---

## Rank Commands

| Command | Description |
|---------|-------------|
| `/ishop rank info` | View your shopper rank |
| `/ishop rank info <player>` | View player's rank |
| `/ishop rank progress` | View progress to next level |

---

## Transaction Log Commands

| Command | Description |
|---------|-------------|
| `/transactionlog reload` | Reload configuration |
| `/transactionlog status` | Show logging status |
| `/transactionlog test <buy\|sell>` | Send test transaction |
| `/transactionlog toggle <file\|discord>` | Toggle logging method |

**Aliases**: `/tlog`, `/translog`

---

## Feature Toggle

```bash
/ishop toggle <feature>
```

Available features:
- `black-market`
- `daily-shop`
- `custom-currencies`
- `loot`
- `multipliers`
- `sign`
- `shopper-rank`
- `item-discount`
- `stack-discount`
- `taxes`
- `dynamic-pricing`
- `frame-shop`
- `player-frame-shop`
- `limited-stock`
- `limited-sell`
- `npc`
- `realistic-season`
- `transaction-logging`

---

## Tips

1. Use **tab completion** for command suggestions
2. Most commands have **shorter aliases**
3. Use `/ishop help <command>` for detailed help
4. Admin commands require **appropriate permissions**
