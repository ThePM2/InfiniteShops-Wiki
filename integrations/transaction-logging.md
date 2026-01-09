# 📋 Transaction Logging

Track all shop transactions for security and analysis!

---

## Overview

Transaction Logging records all buy/sell transactions to files and optionally to Discord. This helps with:

- Tracking player activity
- Detecting exploits
- Analyzing economy flow
- Resolving disputes

---

## Configuration

Edit `plugins/InfiniteShops/transaction-log.yml`:

```yaml
# Transaction Logging Configuration

enabled: true

# File logging
file:
  enabled: true
  # Log file location
  path: "logs/transactions"
  # Date format for file names
  date_format: "yyyy-MM-dd"
  # Log format
  format: "[%time%] %player% %action% %amount%x %item% for %price% (%currency%)"

# Discord logging (requires DiscordSRV)
discord:
  enabled: false
  channel_id: "123456789012345678"
  
  # Embed settings
  embed:
    buy_color: "#00FF00"
    sell_color: "#FF6600"
    show_timestamp: true
    show_location: false
```

---

## File Logging

### Log Location

Logs are stored in:
```
plugins/InfiniteShops/logs/transactions/
├── 2025-01-01.log
├── 2025-01-02.log
└── 2025-01-03.log
```

### Log Format

Each line contains:
```
[12:34:56] Steve BUY 64x Diamond for $6,400.00 (VAULT) @ world:100,64,200
```

### Log Fields

| Field | Description |
|-------|-------------|
| `%time%` | Transaction time |
| `%player%` | Player name |
| `%action%` | BUY or SELL |
| `%amount%` | Item quantity |
| `%item%` | Item name |
| `%price%` | Transaction price |
| `%currency%` | Currency type |
| `%location%` | Shop location |
| `%shop%` | Shop name |

---

## Discord Logging

### Requirements

- [DiscordSRV](https://www.spigotmc.org/resources/discordsrv.18494/)

### Setup

1. Install and configure DiscordSRV
2. Get your channel ID (Developer Mode → Right-click channel → Copy ID)
3. Configure InfiniteShops:

```yaml
discord:
  enabled: true
  channel_id: "123456789012345678"
```

### Embed Format

<!-- 📸 IMAGE PLACEHOLDER: Screenshot of Discord transaction log embed showing buy transaction. Dimensions: 400x250px -->

```yaml
discord:
  embed:
    buy_color: "#00FF00"
    sell_color: "#FF6600"
    
    title: "Transaction Log"
    
    fields:
      player: true
      action: true
      item: true
      amount: true
      price: true
      shop: true
      timestamp: true
```

---

## Commands

| Command | Description |
|---------|-------------|
| `/transactionlog reload` | Reload configuration |
| `/transactionlog status` | Show logging status |
| `/transactionlog test buy` | Send test buy log |
| `/transactionlog test sell` | Send test sell log |
| `/transactionlog toggle file` | Toggle file logging |
| `/transactionlog toggle discord` | Toggle Discord logging |

### Status Command

```
/transactionlog status
```

Output:
```
=== Transaction Logging Status ===
File Logging: Enabled
Discord Logging: Enabled
DiscordSRV Plugin: Available
```

---

## Log Types

### Standard Transactions

Normal buy/sell from GUI shops:

```
[12:34:56] Steve BUY 32x Iron_Ingot for $640.00 (VAULT)
```

### Sign Shop Transactions

```
[12:35:10] Steve SELL 64x Cobblestone for $32.00 (VAULT) [Sign Shop]
```

### NPC Shop Transactions

```
[12:35:45] Steve BUY 1x Diamond_Sword for $500.00 (VAULT) [NPC: Blacksmith]
```

### Black Market Transactions

```
[12:40:00] Steve AUCTION_WIN 1x Netherite_Sword for $15,000.00 (VAULT) [Black Market]
```

### Daily Shop Transactions

```
[12:45:00] Steve BUY 1x Enchanted_Book for $2,500.00 (VAULT) [Daily Shop]
```

---

## Advanced Configuration

### Custom Log Format

```yaml
file:
  format: "%time% | %player% | %action% | %item% x%amount% | %price% %currency%"
```

### Separate Log Files

```yaml
file:
  separate_by_type: true
  # Creates:
  # - transactions/buys/2025-01-01.log
  # - transactions/sells/2025-01-01.log
```

### Log Rotation

```yaml
file:
  rotation:
    enabled: true
    max_files: 30  # Keep 30 days
    compress_old: true
```

---

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `infiniteshops.transactionlog.admin` | Admin commands | op |

---

## Security Notes

1. **Protect log files** - They contain player activity
2. **Regular backups** - Logs are valuable for disputes
3. **Discord channel** - Make it staff-only
4. **Review regularly** - Look for suspicious patterns

---

## Troubleshooting

### Logs Not Creating

1. Check `file.enabled: true`
2. Verify folder permissions
3. Check for disk space

### Discord Not Working

1. Verify DiscordSRV is installed
2. Check channel ID is correct
3. Verify bot has permissions in channel
4. Run `/transactionlog test buy`

---

## Tips

1. **Archive old logs** - Set up log rotation to save space
2. **Staff-only Discord channel** - Protect player activity data
3. **Review weekly** - Look for unusual patterns
4. **Custom format** - Tailor logs to your analysis needs
5. **Backup regularly** - Logs are valuable for dispute resolution
