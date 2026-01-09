# ➕ Plugin Integrations

InfiniteShops works seamlessly with popular plugins!

---

## Economy Plugins

### Vault (Required)

InfiniteShops requires Vault and hooks into any Vault-compatible economy:

- **EssentialsX Economy**
- **CMI Economy**
- **iConomy**
- **And many more...**

### PlayerPoints

Use PlayerPoints as a currency:

```yaml
items:
  special_item:
    material: DIAMOND
    buy_price: 100
    ecoType: PLAYERPOINTS
```

### TokenEnchant

Use TokenEnchant tokens:

```yaml
items:
  enchant_token:
    material: NETHER_STAR
    buy_price: 50
    ecoType: TOKENENCHANT
```

---

## Hologram Plugins

InfiniteShops auto-detects hologram plugins:

### DecentHolograms (Recommended)

```yaml
hologram-handler: DecentHolograms
```

### HolographicDisplays

```yaml
hologram-handler: HolographicDisplays
```

### CMI Holograms

```yaml
hologram-handler: CMI
```

Holograms are used for:
- Frame shop displays
- Sign shop info
- NPC shop labels

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing hologram above a frame shop with pricing info. Dimensions: 500x350px -->

---

## NPC Plugin

### Citizens

Required for NPC shops:

1. Install Citizens
2. Enable NPC feature: `/ishop toggle npc`
3. Create NPCs: `/ishop npc create`

---

## Custom Items Plugins

### ItemsAdder

Use ItemsAdder custom items in shops:

```yaml
items:
  custom_sword:
    itemsadder: 'namespace:custom_sword'
    buy_price: 1000
    ecoType: VAULT
```

### Oraxen

Use Oraxen custom items:

```yaml
items:
  oraxen_item:
    oraxen: 'custom_item_id'
    buy_price: 500
    ecoType: VAULT
```

### Nexo

Use Nexo custom items:

```yaml
items:
  nexo_item:
    nexo: 'item_id'
    buy_price: 750
    ecoType: VAULT
```

---

## Discord Integration

### DiscordSRV

Send transaction logs to Discord:

1. Install DiscordSRV and configure it
2. Enable in InfiniteShops:

```yaml
# In transaction-log.yml
discord:
  enabled: true
  channel_id: "123456789012345678"
  
  # Embed format
  embed:
    color: "#00FF00"  # For buys
    sell_color: "#FF0000"  # For sells
```

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of Discord embed showing a transaction log entry. Dimensions: 400x200px -->

---

## Seasonal Plugins

### RealisticSeasons

Adjust prices based on seasons:

```yaml
features:
  realistic-season: true

seasonal_pricing:
  SPRING:
    crops: 0.8  # 20% cheaper
  SUMMER:
    crops: 0.7
  FALL:
    crops: 1.2  # 20% more expensive
  WINTER:
    crops: 1.5
```

---

## World Management

### Multiverse-Core

InfiniteShops is compatible with Multiverse. Configure per-world shops:

```yaml
items:
  diamond:
    material: DIAMOND
    buy_price: 100
    worlds:
      - world
      - world_nether
    blacklist_worlds:
      - creative_world
```

---

## Permission Plugins

### LuckPerms (Recommended)

```bash
# Give shop access
/lp group default permission set infiniteshops.use true

# Give VIP perks
/lp group vip permission set infiniteshops.dailyshop.vip true
/lp group vip permission set infiniteshops.multiplier.vip true
```

---

## Tool Plugins

### EcoEnchants

EcoEnchants items are fully supported in shops.

### WildTools

WildTools integration for special tool features.

---

## Compatibility Table

| Plugin | Status | Notes |
|--------|--------|-------|
| Vault | ✅ Required | Any Vault economy |
| Citizens | ✅ Supported | For NPC shops |
| PlaceholderAPI | ✅ Supported | Full placeholder support |
| DecentHolograms | ✅ Supported | Recommended hologram |
| HolographicDisplays | ✅ Supported | Alternative hologram |
| CMI | ✅ Supported | Economy + holograms |
| ItemsAdder | ✅ Supported | Custom items |
| Oraxen | ✅ Supported | Custom items |
| Nexo | ✅ Supported | Custom items |
| DiscordSRV | ✅ Supported | Transaction logging |
| RealisticSeasons | ✅ Supported | Seasonal pricing |
| Multiverse-Core | ✅ Compatible | Per-world config |
| LuckPerms | ✅ Compatible | Permissions |
| EcoEnchants | ✅ Compatible | Custom enchants |
| WildTools | ✅ Compatible | Tool features |
| PlayerPoints | ✅ Supported | Currency |
| TokenEnchant | ✅ Supported | Currency |

---

## Adding Integrations

If you need integration with a plugin not listed:

1. Join our Discord
2. Create a feature request
3. Provide plugin details

---

## Troubleshooting

### Plugin Not Detected

1. Check plugin is installed and enabled
2. Check load order (InfiniteShops loads POSTWORLD)
3. Restart server (not reload)

### Custom Items Not Showing

1. Verify item ID is correct
2. Check custom items plugin is loaded
3. Test with `/itemsadder give` or equivalent

---

## Tips

1. **Use DecentHolograms** - Best performance and features
2. **Test integrations** - Verify after server updates
3. **Check compatibility** - Review plugin versions
4. **Enable debug mode** - Helps identify hook issues
5. **Join Discord** - Get help with specific integrations
