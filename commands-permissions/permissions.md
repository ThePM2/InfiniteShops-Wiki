# 🔐 Permissions

Complete reference for all InfiniteShops permissions.

---

## Overview

InfiniteShops uses a comprehensive permission system. Permissions are organized by feature for easy management.

---

## General Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.use` | Access the shop | true |
| `infiniteshops.admin` | All admin permissions | op |

---

## Shop Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.shop.use` | Open shops | true |
| `infiniteshops.shop.buy` | Buy items | true |
| `infiniteshops.shop.sell` | Sell items | true |
| `infiniteshops.shop.sellall` | Use sell all feature | true |
| `infiniteshops.shop.<name>` | Access specific shop | true |

---

## Editor Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.editor` | Access shop editor | op |
| `infiniteshops.editor.create` | Create new shops | op |
| `infiniteshops.editor.delete` | Delete shops | op |
| `infiniteshops.editor.modify` | Modify existing shops | op |

---

## Black Market Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.blackmarket.use` | Access Black Market | true |
| `infiniteshops.blackmarket.bid` | Place bids | true |
| `infiniteshops.blackmarket.admin` | Admin commands | op |
| `infiniteshops.blackmarket.*` | All Black Market perms | op |

---

## Daily Shop Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.dailyshop.use` | Use the Daily Shop | true |
| `infiniteshops.dailyshop.vip` | VIP benefits & preview | false |
| `infiniteshops.dailyshop.bypass.limit` | Bypass purchase limits | false |
| `infiniteshops.dailyshop.admin` | Admin commands | op |
| `infiniteshops.dailyshop.*` | All Daily Shop perms | op |

---

## Sign Shop Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.sign` | Create/manage sign shops | op |
| `infiniteshops.sign.use` | Use sign shops | true |
| `infiniteshops.sign.bypass` | Bypass sign restrictions | op |

---

## NPC Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.npc` | Create/manage NPCs | op |
| `infiniteshops.npc.menu` | Access NPC list | op |
| `infiniteshops.npc.settings` | Modify NPC settings | op |
| `infiniteshops.npc.teleport` | Teleport to NPCs | op |

---

## Frame Shop Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.frame` | Create admin frame shops | op |
| `infiniteshops.frame.player` | Create player frame shops | true |
| `infiniteshops.frame.remove` | Remove frame shops | op |

---

## Loot Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.loot.admin` | Admin loot commands | op |
| `infiniteshops.loot.menu` | Access loot menu | true |
| `infiniteshops.loot.preview` | Preview rewards | true |

---

## Economy Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.multipliers` | Manage multipliers | op |
| `infiniteshops.rank.self` | View own rank | true |
| `infiniteshops.rank.other` | View others' ranks | true |
| `infiniteshops.rank.admin` | Admin rank commands | op |

---

## Multiplier Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.multiplier.vip` | VIP multiplier (auto) | false |
| `infiniteshops.multiplier.vipplus` | VIP+ multiplier (auto) | false |
| `infiniteshops.multiplier.mvp` | MVP multiplier (auto) | false |

---

## Tax Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.tax.bypass` | Bypass all taxes | op |
| `infiniteshops.tax.vip` | Reduced taxes (VIP) | false |
| `infiniteshops.tax.mvp` | Reduced taxes (MVP) | false |

---

## Feature Toggle Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.features.toggle` | Toggle features | op |

---

## Transaction Log Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.transactionlog.admin` | Admin transaction log | op |

---

## Content & Conversion

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.content.view` | View content | op |
| `infiniteshops.convert` | Convert from other plugins | op |

---

## Wildcard Permissions

| Permission | Description |
|------------|-------------|
| `infiniteshops.*` | All InfiniteShops permissions |
| `infiniteshops.admin` | All admin permissions |
| `infiniteshops.blackmarket.*` | All Black Market permissions |
| `infiniteshops.dailyshop.*` | All Daily Shop permissions |

---

## Example LuckPerms Setup

### Default Player

```bash
/lp group default permission set infiniteshops.use true
/lp group default permission set infiniteshops.shop.use true
/lp group default permission set infiniteshops.shop.buy true
/lp group default permission set infiniteshops.shop.sell true
/lp group default permission set infiniteshops.blackmarket.use true
/lp group default permission set infiniteshops.dailyshop.use true
```

### VIP Rank

```bash
/lp group vip parent add default
/lp group vip permission set infiniteshops.dailyshop.vip true
/lp group vip permission set infiniteshops.multiplier.vip true
/lp group vip permission set infiniteshops.tax.vip true
```

### Admin Rank

```bash
/lp group admin permission set infiniteshops.* true
```

---

## Permission Nodes by File

Permissions are defined in `plugins/InfiniteShops/permissions.yml`:

```yaml
BLACK_MARKET: 'infiniteshops.blackmarket.admin'
BLACK_MARKET_BID: 'infiniteshops.blackmarket.bid'
CONTENT: 'infiniteshops.content.view'
CONVERT: 'infiniteshops.convert'
DAILY_SHOP: 'infiniteshops.dailyshop.admin'
DAILY_SHOP_PREVIEW: 'infiniteshops.dailyshop.preview'
DAILY_SHOP_USE: 'infiniteshops.dailyshop.use'
DAILY_SHOP_VIP: 'infiniteshops.dailyshop.vip'
EDITOR: 'infiniteshops.editor'
FRAME: 'infiniteshops.frame'
LOOT: 'infiniteshops.loot.admin'
LOOT_MENU: 'infiniteshops.loot.menu'
LOGGER: 'infiniteshops.logger'
MULTIPLIERS: 'infiniteshops.multipliers'
NPC: 'infiniteshops.npc'
NPC_MENU: 'infiniteshops.npc.menu'
NPC_SETTINGS: 'infiniteshops.npc.settings'
SIGN: 'infiniteshops.sign'
SIGN_CHEST_BYPASS: 'infiniteshops.sign.bypass'
RANK: 'infiniteshops.rank.self'
RANK_OTHER: 'infiniteshops.rank.other'
TOGGLE: 'infiniteshops.features.toggle'
TRANSACTION_LOG: 'infiniteshops.transactionlog.admin'
```

---

## Tips

1. Use **wildcard permissions** for admins
2. Test permissions on a **test account** first
3. Use **permission inheritance** (groups)
4. Document your **permission setup**
5. Review permissions after **updates**
