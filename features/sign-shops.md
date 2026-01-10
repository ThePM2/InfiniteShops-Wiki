# 🪧 Sign Shops

Classic sign-based shops for quick and accessible trading!

---

## Overview

Sign Shops provide a traditional Minecraft shop experience using signs. Players interact with signs to buy or sell items without opening a GUI. Perfect for spawn shops, admin stores, or quick-access trading posts.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing multiple sign shops on a wall with different items and prices displayed. Dimensions: 800x400px -->

---

## Admin Sign Types

| Type | Identifier | Description |
|------|------------|-------------|
| `ADMIN_SHOP` | `Admin-Shop` | Buy and sell items |
| `ADMIN_SELL` | `Admin-Sell` | Sell items only |
| `ADMIN_BUY` | `Admin-Buy` | Buy items only |
| `COMMAND` | `Command` | Execute free commands |
| `COMMAND` | `Command-Shop` | Execute paid commands |
| `FREE` | `Free` | Free item distribution |
| `DISPOSAL` | `Disposal` | Trash bin |
| `ENCHANT` | `Enchant` | Free enchanting |
| `ENCHANT` | `Enchant-Buy` | Paid enchanting |

> 💡 Looking for player-owned shops? See [Player Shops](player-shops.md)

---

## Creating Sign Shops

### Admin Shop (Buy & Sell)

Players can buy AND sell items:

```
Admin-Shop
<amount> <material>
s:<sellPrice> b:<buyPrice>
<ecoType>
```

**Example:**
```
Admin-Shop
64 DIAMOND
s:50 b:100
VAULT
```

- **Line 1**: `Admin-Shop` (identifier)
- **Line 2**: Amount and material (e.g., `64 DIAMOND`)
- **Line 3**: Sell price and buy price (e.g., `s:50 b:100`)
- **Line 4**: Economy type (`VAULT`, `EXP`, or custom currency ID)

**Click Actions:**
| Action | Result |
|--------|--------|
| Left Click | Sell items |
| Right Click | Buy items |
| Shift + Left Click | Sell all |

---

### Admin Sell Only

Players can only sell items to the shop:

```
Admin-Sell
<amount> <material>
s:<sellPrice>
<ecoType>
```

**Example:**
```
Admin-Sell
32 IRON_INGOT
s:10
VAULT
```

**Click Actions:**
| Action | Result |
|--------|--------|
| Left Click | Sell items |
| Shift + Left Click | Sell all |

---

### Admin Buy Only

Players can only buy items from the shop:

```
Admin-Buy
<amount> <material>
b:<buyPrice>
<ecoType>
```

**Example:**
```
Admin-Buy
16 GOLD_INGOT
b:25
VAULT
```

**Click Actions:**
| Action | Result |
|--------|--------|
| Click | Buy items |

---

## Command Signs

### Free Command Sign

Execute commands for free when clicked:

```
Command
<executor>
<display text>

```

**Example:**
```
Command
CONSOLE
&aFree Diamonds!

```

- **Line 2**: `CONSOLE` or `PLAYER` (who runs the command)
- **Line 3**: Display text shown on the sign
- **Line 4**: Leave empty

After placing, add commands with:
```
/ishop sign command add give %player% diamond 1
```

---

### Paid Command Sign

Execute commands for a price:

```
Command-Shop
<executor> <display text>
b:<price>
<ecoType>
```

**Example:**
```
Command-Shop
CONSOLE &aVIP Kit
b:1000
VAULT
```

Then add the command:
```
/ishop sign command add lp user %player% parent set vip
```

---

## Free Item Signs

Give items to players for free:

```
Free
<material>
<rows>

```

**Example:**
```
Free
DIAMOND
3

```

- **Line 2**: Material to give (e.g., `DIAMOND`)
- **Line 3**: Number of inventory rows (1-6)

This opens a GUI where players can take free items.

---

## Free Item Sign (Custom Item)

Use an item from your hand:

```
Free-Item
<item>
<rows>

```

After placing, hold the item you want to give and run:
```
/ishop sign set item
```

---

## Disposal Sign

Create a trash bin for players:

```
Disposal



```

Just write `Disposal` on line 1, leave the rest empty.

Opens a disposal GUI where players can throw away unwanted items.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of disposal inventory GUI with items being thrown away. Dimensions: 400x300px -->

---

## Enchantment Signs

### Free Enchanting

Apply enchantments for free:

```
Enchant
<enchantment>
<level>
<allow_any_item>
```

**Example:**
```
Enchant
SHARPNESS
5
false
```

- **Line 2**: Enchantment name (e.g., `SHARPNESS`, `UNBREAKING`)
- **Line 3**: Enchantment level
- **Line 4**: `true` = allow enchanting any item, `false` = only valid items

---

### Paid Enchanting

Charge for enchantments:

```
Enchant-Buy
<enchantment> <level>
b:<price>
<allow_any_item> <ecoType>
```

**Example:**
```
Enchant-Buy
SHARPNESS 5
b:5000
false VAULT
```

---

## Sign Appearance

After creation, signs transform to a formatted display:

**Admin-Shop becomes:**
```
[Shop]
64x DIAMOND
Sell: 50 VAULT
Buy: 100 VAULT
```

**Command becomes:**
```
[Command]

Free Diamonds!

```

You can customize these formats in `signs.yml`.

---

## Sign Commands

| Command | Description |
|---------|-------------|
| `/ishop sign create <type>` | Create sign by looking at it |
| `/ishop sign set <property> <value>` | Set sign properties |
| `/ishop sign command add <command>` | Add command to sign |
| `/ishop sign command remove <index>` | Remove command by index |
| `/ishop sign command list` | List commands on sign |
| `/ishop sign info` | View sign information |

---

## Permissions

| Permission | Description |
|------------|-------------|
| `infiniteshops.admin.shop` | Create Admin-Shop signs |
| `infiniteshops.admin.sell` | Create Admin-Sell signs |
| `infiniteshops.admin.buy` | Create Admin-Buy signs |
| `infiniteshops.admin.command` | Create Command signs |
| `infiniteshops.admin.free` | Create Free item signs |
| `infiniteshops.admin.disposal` | Create Disposal signs |
| `infiniteshops.admin.enchant` | Create Enchant signs |
| `infiniteshops.sign` | General sign management |
| `infiniteshops.sign.bypass` | Bypass sign protections |

---

## Configuration

### signs.yml

Customize sign formats and behavior:

```yaml
# Split material names (DIAMOND_SWORD → Diamond Sword)
split_materials_name: true

# Display item above sign
display_material_above_sign: true

# Show actions in action bar
display_actions_to_action_bar: true

# Require confirmation before breaking
require_confirmation_on_break: true

# Action bar format
actions_bar: '&f%identifier% &6%description% '

# GUI titles
free_title: '&aFree %material%'
disposal_title: '&6Disposal'
```

### Enchantment Shortcuts

Define shortcuts for long enchantment names:

```yaml
placeholders:
  enchants:
    unb: 'UNBREAKING'
    eff: 'EFFICIENCY'
    sharp: 'SHARPNESS'
```

Now you can use `unb` instead of `UNBREAKING` on signs.

### Material Shortcuts

Define shortcuts for materials:

```yaml
placeholders:
  materials:
    DIAMOND: 'DMD'
    NETHERITE: 'NETH'
```

---

## Item Display Offset

Customize floating item position above signs:

```yaml
offset_item:
  wall_x: 0.0625
  wall_y: 0.8
  wall_z: 0.0625
  x: 0.5
  y: 1.1
  z: 0.5
```

---

## Tips

> 💡 **Use shortcuts** to fit long names on signs (configure in signs.yml)

> 💡 **Display items** appear floating above signs for easy identification

> 💡 **Action bar** shows players what each click does

> 💡 **Shift-click** to sell all matching items at once

> 💡 **Test signs** in a private area before placing in public

---

## See Also

- [Player Shops](player-shops.md) - Player-owned chest shops
- [Currencies](../economy/currencies.md) - Economy types
- [Permissions](../commands-permissions/permissions.md) - All permissions
