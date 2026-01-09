# ❓ FAQ & Troubleshooting

Answers to common questions and solutions to frequent issues.

---

## Frequently Asked Questions

### General

#### What Minecraft versions are supported?

InfiniteShops supports Minecraft 1.20 through 1.21.x. Both Spigot and Paper (and their forks) are fully supported.

#### What are the required dependencies?

- **ProtocolLib** - Required for packet handling
- **Vault** - Required for economy integration
- An economy plugin (EssentialsX, CMI, etc.)

#### Can I use multiple economy plugins?

Yes! InfiniteShops supports multiple economy types per item. You can mix Vault, EXP, custom currencies, and item currencies in the same shop.

---

### Shops

#### How do I create a new shop?

1. Create a YAML file in `plugins/InfiniteShops/shops/`
2. Or use the in-game editor: `/ishop editor`
3. Reload with `/ishop reload`

See [Basic Configuration](configuration.md) for detailed instructions.

#### Can players create their own shops?

Yes! Frame shops can be configured to allow player-owned shops. Enable `player_frame_shop` in config.yml.

#### How many items can a shop have?

There's no hard limit. For shops with many items, pagination is automatically enabled.

---

### Economy

#### How do I set up custom currencies?

Create a currency file in `plugins/InfiniteShops/currencies/`:

```yaml
# currencies/gems.yml
name: 'Gems'
symbol: '💎'
starting_balance: 0
```

See [Currencies](economy/currencies.md) for complete setup.

#### Why aren't prices showing correctly?

1. Check your `ecoType_placeholders` in config.yml
2. Verify PlaceholderAPI is installed for balance placeholders
3. Ensure your economy plugin is properly hooked

---

### Black Market

#### How do I start a Black Market event?

- **Automatic**: Enable `full_moon: true` for moon-based triggers
- **Manual**: Use `/blackmarket start`
- **Scheduled**: Configure times in `auto_open.schedule`

#### Can I have multiple Black Markets?

Currently, only one Black Market event can run at a time, but you can create multiple item pools that rotate.

---

## Troubleshooting

### Plugin Won't Enable

**Symptoms**: Plugin shows as red in `/plugins` or error on startup

**Solutions**:
1. Check Java version: Must be Java 17+
   ```
   java -version
   ```
2. Verify ProtocolLib is installed and enabled
3. Check for startup errors in console
4. Ensure the JAR file isn't corrupted (re-download)

---

### Economy Not Working

**Symptoms**: Players can't buy/sell, balance shows as 0

**Solutions**:

1. **Check Vault integration**:
   ```
   /vault-info
   ```
   
2. **Verify economy plugin**:
   - Is your economy plugin enabled?
   - Does it support Vault?
   
3. **Check permissions**:
   - Player needs `infiniteshops.shop.use`
   
4. **Review console**:
   - Look for "Successfully hooked into Vault" on startup

---

### Shops Not Opening

**Symptoms**: `/shop` command does nothing or shows error

**Solutions**:

1. **Check permissions**:
   ```yaml
   infiniteshops.shop.use: true
   infiniteshops.shop.<shopname>: true
   ```

2. **Verify shop file exists**:
   - Check `plugins/InfiniteShops/shops/`
   - File must have `.yml` extension

3. **Validate YAML syntax**:
   - Use an online YAML validator
   - Check for tab characters (use spaces only)

4. **Reload the plugin**:
   ```
   /ishop reload
   ```

---

### NPCs Not Working

**Symptoms**: NPCs don't respond to clicks, won't spawn

**Solutions**:

1. **Verify Citizens is installed**:
   ```
   /plugins
   ```
   
2. **Check NPC permissions**:
   ```yaml
   infiniteshops.npc.use: true
   ```
   
3. **Re-link the NPC**:
   ```
   /ishop npc link <shop>
   ```

---

### Holograms Not Showing

**Symptoms**: No text above sign/frame shops

**Solutions**:

1. **Check hologram plugin**:
   - DecentHolograms, HolographicDisplays, or CMI required
   
2. **Verify auto-detection**:
   - Leave `hologram-handler` empty in config.yml
   
3. **Check hologram settings**:
   ```yaml
   sign_shops:
     hologram:
       enabled: true
   ```

---

### Transaction Logging Not Working

**Symptoms**: No logs in file or Discord

**Solutions**:

1. **Enable the feature**:
   ```yaml
   features:
     transaction-logging: true
   ```

2. **For Discord logging**:
   - Verify DiscordSRV is installed
   - Check webhook URL is correct
   - Test with `/transactionlog test buy`

3. **Check file permissions**:
   - Ensure server can write to logs directory

---

### Performance Issues

**Symptoms**: Lag when opening shops, slow transactions

**Solutions**:

1. **Use MySQL for large servers**:
   ```yaml
   database:
     type: MySQL
   ```

2. **Reduce hologram updates**:
   ```yaml
   hologram:
     update_interval: 100  # ticks
   ```

3. **Limit search results**:
   ```yaml
   search:
     max_results: 50
   ```

4. **Disable unused features**:
   ```yaml
   features:
     dynamic-pricing: false
     realistic-season: false
   ```

---

### YAML Syntax Errors

**Symptoms**: Plugin fails to load configs, errors mention "parsing"

**Common Mistakes**:

| Wrong | Correct |
|-------|---------|
| Using tabs | Use spaces (2 or 4) |
| `name: Player's Shop` | `name: "Player's Shop"` |
| Missing quotes on special chars | Quote strings with `:`, `#`, `&` |
| Inconsistent indentation | Keep indentation consistent |

**Example of correct YAML**:
```yaml
items:
  diamond:
    material: DIAMOND
    name: '&bShiny Diamond'  # Quoted for color codes
    buy_price: 100
    sell_price: 50
```

---

## Getting Help

If you can't solve your issue:

1. **Check the wiki** - Most answers are here
2. **Enable debug mode**:
   ```yaml
   debug: true
   ```
3. **Join Discord** - Get community support
4. **Report bugs** - Use GitHub Issues with:
   - Server version
   - Plugin version
   - Full error log
   - Steps to reproduce

---

## Migrating from Other Plugins

### From EssentialsX Worth

InfiniteShops can import your item prices:

```
/ishop convert essentials
```

### From ShopGUI+

```
/ishop convert shopguiplus
```

### From BossShopPro

```
/ishop convert bossshoppro
```

### Manual Migration

If automatic conversion isn't available:

1. Export your old shop data
2. Create new shop files in `plugins/InfiniteShops/shops/`
3. Map your items and prices manually
4. Test thoroughly before going live

---

## Tips for Success

1. **Always backup** before making changes
2. **Test on development server** first
3. **Read error messages** - They often tell you exactly what's wrong
4. **Keep plugins updated** - Including dependencies
5. **Use the in-game editor** when possible - Reduces YAML errors
