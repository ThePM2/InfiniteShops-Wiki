# 💾 First Install

Get InfiniteShops up and running on your server in minutes!

---

## Prerequisites

Before installing InfiniteShops, ensure you have the following:

| Requirement | Details |
|-------------|---------|
| **Server Software** | Spigot, Paper, or any fork (1.20 - 1.21.x) |
| **Java** | Java 17 or higher |
| **ProtocolLib** | [Download here](https://www.spigotmc.org/resources/protocollib.1997/) |
| **Vault** | [Download here](https://www.spigotmc.org/resources/vault.34315/) |
| **Economy Plugin** | EssentialsX, CMI, or any Vault-compatible economy |

---

## Step 1: Download Required Plugins

### ProtocolLib (Required)

1. Download the latest version from SpigotMC
2. Place `ProtocolLib.jar` in your `plugins/` folder

### Vault (Required)

1. Download the latest version from SpigotMC
2. Place `Vault.jar` in your `plugins/` folder

### Economy Plugin

Install one of these economy plugins:
- **EssentialsX** (recommended)
- **CMI**
- **Any Vault-compatible economy**

---

## Step 2: Install InfiniteShops

1. Download `InfiniteShops.jar` from SpigotMC
2. Place it in your `plugins/` folder
3. Restart your server (not reload!)

<!-- 📸 IMAGE PLACEHOLDER: Screenshot showing the plugins folder with all required jars highlighted. Dimensions: 800x400px -->

---

## Step 3: Verify Installation

After server restart, check your console for:

```
[InfiniteShops] Enabling InfiniteShops
[InfiniteShops] Successfully hooked into Vault economy
[InfiniteShops] InfiniteShops has been enabled!
```

You can also run `/ishop` in-game to verify the plugin is working.

<!-- 📸 GIF PLACEHOLDER: Animation showing the /ishop command being executed and the main menu opening. Dimensions: 600x400px -->

---

## Step 4: Initial Setup

### Open the Main Menu

Use one of these commands:
- `/shop` - Opens the main shop menu
- `/ishop` - Opens admin controls

### Default Files Created

InfiniteShops will generate the following files in `plugins/InfiniteShops/`:

```
InfiniteShops/
├── config.yml           # Main configuration
├── messages.yml         # All plugin messages
├── permissions.yml      # Permission definitions
├── shops/               # Shop category files
│   └── example.yml
├── blackmarket/         # Black market configuration
├── dailyshop/          # Daily shop settings
├── currencies/          # Custom currency definitions
└── loot/               # Loot crate configurations
```

---

## Optional Features

Enable additional features by installing optional plugins:

### NPC Shops
Install **Citizens** to create NPC-based shops:
```
/ishop npc create <name>
```

### Holograms
Install one of these for shop holograms:
- DecentHolograms (recommended)
- HolographicDisplays
- CMI Holograms

### Custom Items
Support for custom item plugins:
- ItemsAdder
- Oraxen
- Nexo

---

## Quick Start Commands

| Command | Description |
|---------|-------------|
| `/shop` | Open the main shop menu |
| `/ishop help` | View all admin commands |
| `/ishop reload` | Reload configuration files |
| `/ishop editor` | Open the in-game shop editor |

---

## Troubleshooting

### Plugin Not Loading

1. Check Java version: `java -version` (must be 17+)
2. Verify ProtocolLib is installed
3. Check for errors in console

### Economy Not Working

1. Ensure Vault is installed
2. Verify your economy plugin is loaded
3. Check `/vault-info` for economy status

### Shops Not Opening

1. Check player permissions
2. Verify shop files are valid YAML
3. Use `/ishop reload` after changes

---

## Tips

1. **Start simple** - Get basic shops working before adding advanced features
2. **Test on local server** - Configure everything before going live
3. **Backup configs** - Always backup before major changes
4. **Read the docs** - This wiki covers all features in detail
5. **Use tab completion** - Commands support tab completion for easy use

---

## Next Steps

Now that InfiniteShops is installed, you can:

1. [Configure your shops](configuration.md)
2. [Set up the Black Market](../features/black-market.md)
3. [Create NPC merchants](../features/npc-shops.md)
4. [Configure currencies](../economy/currencies.md)

---

> 💡 **Need Help?** Join our Discord server for support!
