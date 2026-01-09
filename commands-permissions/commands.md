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
| `/ishop create <name>` | Create a new shop category |
| `/ishop delete <name>` | Delete a shop category |
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

**Aliases**: `/bm`, `/blackm`

---

## Daily Shop Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/dailyshop` | Open Daily Shop | `infiniteshops.dailyshop.use` |
| `/dailyshop help` | Show help menu | `infiniteshops.dailyshop.use` |
| `/dailyshop stats` | View your statistics | `infiniteshops.dailyshop.use` |
| `/dailyshop history` | View purchase history | `infiniteshops.dailyshop.use` |
| `/dailyshop preview` | Preview upcoming items | `infiniteshops.dailyshop.vip` |
| `/dailyshop reload` | Reload configuration | `infiniteshops.dailyshop.admin` |
| `/dailyshop reset <type>` | Reset items (daily/weekly/all) | `infiniteshops.dailyshop.admin` |
| `/dailyshop toggle` | Enable/disable shop | `infiniteshops.dailyshop.admin` |

**Aliases**: `/ds`, `/dshop`

---

## NPC Commands

| Command | Description |
|---------|-------------|
| `/ishop npc create` | Open NPC creation menu |
| `/ishop npc create <type> <shop> [name]` | Quick create NPC |
| `/ishop npc link <shop>` | Link selected NPC to shop |
| `/ishop npc unlink` | Remove shop link from NPC |
| `/ishop npc list` | View all NPC shops |
| `/ishop npc remove <id>` | Remove an NPC |
| `/ishop npc settings` | Open NPC settings GUI |
| `/ishop npc type <entityType>` | Change NPC entity type |
| `/ishop npc teleport <id>` | Teleport to NPC |

---

## Sign Shop Commands

| Command | Description |
|---------|-------------|
| `/ishop sign create <type>` | Create a sign shop |
| `/ishop sign set <option> <value>` | Set sign option |
| `/ishop sign info` | View sign information |
| `/ishop sign remove` | Remove sign shop |
| `/ishop sign command add <cmd>` | Add command to sign |
| `/ishop sign command remove <index>` | Remove command |
| `/ishop sign command list` | List all commands |

### Sign Set Options

| Option | Values | Description |
|--------|--------|-------------|
| `material` | Any material | Item being traded |
| `amount` | Number | Quantity per transaction |
| `buyPrice` | Number | Price to buy |
| `sellPrice` | Number | Price to sell |
| `ecoType` | VAULT/EXP/ITEM/CUSTOM | Economy type |
| `displayItem` | Any material | Displayed item |
| `level` | true/false | Use XP levels |
| `commandExecutor` | PLAYER/CONSOLE | Who runs commands |

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
| `/ishop loot create <name>` | Create new loot config |
| `/ishop loot open <loot> [player]` | Open a loot crate |
| `/ishop loot give <loot> <player> [amount]` | Give loot keys |
| `/ishop loot preview <loot>` | Preview possible rewards |
| `/ishop loot reload` | Reload loot configurations |

---

## Currency Commands

| Command | Description |
|---------|-------------|
| `/ishop currency <name> balance` | Check your balance |
| `/ishop currency <name> balance <player>` | Check player's balance |
| `/ishop currency <name> give <player> <amount>` | Give currency |
| `/ishop currency <name> take <player> <amount>` | Take currency |
| `/ishop currency <name> set <player> <amount>` | Set balance |
| `/ishop currency <name> top` | View leaderboard |
| `/ishop currency <name> withdraw <amount>` | Withdraw to item |

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
| `/ishop rank` | View your shopper rank |
| `/ishop rank <player>` | View player's rank |
| `/ishop rank top` | View leaderboard |
| `/ishop rank set <player> <rank>` | Set player's rank (admin) |
| `/ishop rank reset <player>` | Reset player's progress (admin) |

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
