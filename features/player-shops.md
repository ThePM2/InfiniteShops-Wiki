# Player Shops (Chest Shops)

Allow players to create their own shops using signs and chests!

---

## Overview

Player Shops let your players become merchants by creating sign-based shops attached to containers. Items are stocked from the player's chest, and money transfers automatically between buyers and sellers.

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of a marketplace area with multiple player-owned chest shops showing different items and prices. Dimensions: 800x450px -->

---

## Shop Types

| Type | Identifier | Description |
|------|------------|-------------|
| **Buy & Sell** | `Chest-Shop` | Players can buy from AND sell to the shop |
| **Buy Only** | `Buy` | Players can only buy from the shop |
| **Sell Only** | `Sell` | Players can only sell to the shop |

---

## Creating a Player Shop

### Chest-Shop (Buy & Sell)

1. Place a chest with items you want to sell
2. Place a sign on the chest
3. Write:

```
Chest-Shop
<amount>
s:<sellPrice> b:<buyPrice>
<ecoType>
```

**Example:**
```
Chest-Shop
64
s:50 b:100
VAULT
```

This creates a shop where:
- Players **sell** 64 items to you for $50
- Players **buy** 64 items from you for $100

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing a Chest-Shop sign on a chest with formatted prices displayed. Dimensions: 500x400px -->

---

### Buy-Only Shop

Players can only purchase items from your chest:

```
Buy
<amount>
b:<buyPrice>
<ecoType>
```

**Example:**
```
Buy
32
b:500
VAULT
```

---

### Sell-Only Shop

Players can only sell items to your chest:

```
Sell
<amount>
s:<sellPrice>
<ecoType>
```

**Example:**
```
Sell
16
s:25
VAULT
```

---

## How It Works

1. **Owner stocks the chest** with items to sell
2. **Sign is placed** on the container
3. **Sign transforms** to show formatted prices and owner name
4. **Buyers interact** with the sign to purchase
5. **Money transfers** from buyer to chest owner
6. **Items transfer** from chest to buyer's inventory

### After Creation

The sign transforms to show:
```
[ChestShop]

Sell: 50 VAULT
Buy: 100 VAULT
YourName
```

<!-- 📸 GIF PLACEHOLDER: Animation showing player creating a chest shop - placing chest, adding items, placing sign, and sign transforming. Dimensions: 600x400px -->

---

## Permissions

| Permission | Description |
|------------|-------------|
| `infiniteshops.player.shop` | Create buy & sell chest shops |
| `infiniteshops.player.buy` | Create buy-only chest shops |
| `infiniteshops.player.sell` | Create sell-only chest shops |
| `infiniteshops.sign.bypass` | Access other players' chest shops as admin |

---

## Supported Containers

Player shops work with:
- Chests
- Trapped Chests
- Barrels
- Shulker Boxes
- Double Chests

---

## Currency Types

You can use different economy types on Line 4:

| Type | Description |
|------|-------------|
| `VAULT` | Standard economy (EssentialsX, CMI, etc.) |
| `EXP` | Experience points |
| `PLAYERPOINTS` | PlayerPoints plugin |
| Custom currency ID | Your custom currencies |

---

## Click Actions

| Action | Result |
|--------|--------|
| **Left Click** | Sell items to the shop |
| **Right Click** | Buy items from the shop |

---

## Protection

- Only the **shop owner** can open the chest
- Admins with `infiniteshops.sign.bypass` can access any chest shop
- Breaking the sign removes the shop
- Confirmation is required before breaking (configurable)

---

## Configuration

In `config.yml`:

```yaml
# Require confirmation before breaking shop signs
require_confirmation_on_break: true

# Display settings
chest_shop_display_name: '&f%amount%x'
default_cage_item: WHITE_STAINED_GLASS
```

In `signs.yml` you can customize the sign appearance:

```yaml
chest_shop:
  identifier: 'Chest-Shop'
  lines:
    - 'Chest-Shop'
    - '%amount%'
    - 's:%sellPrice% b:%buyPrice%'
    - '%ecoType%'
  lines_after_processing:
    - '&7[&aChestShop&7]'
    - '&aSell: %sellPrice%%ecoType%'
    - '&cBuy: %buyPrice%%ecoType%'
    - '&f%owner%'
  sign_type: PLAYER_SHOP
  permission: infiniteshops.player.shop
```

---

## Tips

> 💡 **Stock Management**: Keep your chest stocked! Empty chests can't sell items.

> 💡 **Pricing Strategy**: Set buy prices higher than sell prices to make profit.

> 💡 **Location Matters**: Place shops in high-traffic areas for more sales.

> 💡 **Use Double Chests**: More storage = less restocking needed.

> 💡 **Multiple Shops**: Create separate shops for different items.

---

## Troubleshooting

### "This Chest Shop is empty!"
The chest has no items matching the shop's item type.

### Sign doesn't transform
- Check you have the correct permission
- Verify the format is exactly as shown above
- Make sure the sign is attached to a valid container

### Can't access my own chest
The sign might not have registered you as owner. Break and recreate it.

---

## See Also

- [Sign Shops](sign-shops.md) - Admin sign shops
- [Currencies](../economy/currencies.md) - Custom economy types
- [Permissions](../commands-permissions/permissions.md) - All permissions
