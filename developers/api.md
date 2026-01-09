# 🔧 API

Developer API documentation for InfiniteShops.

---

## Overview

InfiniteShops provides a comprehensive API for developers to integrate with the plugin's features programmatically.

---

## Maven / Gradle

> ⚠️ **Note**: Replace the repository URL with the actual InfiniteShops repository once published.

### Maven

```xml
<repository>
    <id>infiniteshops</id>
    <url>https://repo.infiniteshops.net/releases</url>
</repository>

<dependency>
    <groupId>com.infiniteshops</groupId>
    <artifactId>InfiniteShops</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```

### Gradle

```groovy
repositories {
    maven { url 'https://repo.infiniteshops.net/releases' }
}

dependencies {
    compileOnly 'com.infiniteshops:InfiniteShops:1.0.0'
}
```

---

## Getting the API

```java
import com.infiniteshops.api.InfiniteShopsAPI;

public class MyPlugin extends JavaPlugin {
    
    private InfiniteShopsAPI api;
    
    @Override
    public void onEnable() {
        // Get the API instance
        api = InfiniteShopsAPI.getInstance();
        
        if (api == null) {
            getLogger().severe("InfiniteShops not found!");
            return;
        }
    }
}
```

---

## Shop API

### Opening Shops

```java
// Open a shop for a player
api.openShop(player, "myShop");

// Open a specific category
api.openShop(player, "myShop", "weapons");

// Open Daily Shop
api.openDailyShop(player);

// Open Black Market
api.openBlackMarket(player);
```

### Shop Information

```java
// Get all registered shops
List<Shop> shops = api.getShops();

// Get a specific shop
Shop shop = api.getShop("myShop");

// Check if shop exists
boolean exists = api.shopExists("myShop");
```

---

## Economy API

### Balance Operations

```java
// Get player balance (Vault)
double balance = api.getBalance(player);

// Check if player can afford
boolean canAfford = api.canAfford(player, 1000.0);

// Withdraw money
api.withdraw(player, 1000.0);

// Deposit money
api.deposit(player, 500.0);
```

### Custom Currencies

```java
// Get custom currency balance
int customBalance = api.getCustomCurrencyBalance(player, "gems");

// Add custom currency
api.addCustomCurrency(player, "gems", 100);

// Remove custom currency
api.removeCustomCurrency(player, "gems", 50);
```

---

## Transaction API

### Processing Transactions

```java
// Create a buy transaction
TransactionResult result = api.processBuy(player, shopItem, amount);

if (result.isSuccess()) {
    // Transaction successful
} else {
    // Handle failure
    String reason = result.getFailureReason();
}

// Create a sell transaction
TransactionResult sellResult = api.processSell(player, item, amount);
```

### Transaction History

```java
// Get player's transaction history
List<Transaction> history = api.getTransactionHistory(player);

// Get transactions for a specific shop
List<Transaction> shopHistory = api.getTransactionHistory(player, "myShop");
```

---

## Multiplier API

```java
// Add a buy multiplier
api.addMultiplier(player, MultiplierType.BUY, 1.5, 3600); // 1.5x for 1 hour

// Add a sell multiplier
api.addMultiplier(player, MultiplierType.SELL, 2.0, 7200); // 2x for 2 hours

// Get active multipliers
List<Multiplier> multipliers = api.getActiveMultipliers(player);

// Remove all multipliers
api.clearMultipliers(player);
```

---

## Shopper Rank API

```java
// Get player's shopper rank
ShopperRank rank = api.getShopperRank(player);

// Get loyalty points
int points = api.getLoyaltyPoints(player);

// Add loyalty points
api.addLoyaltyPoints(player, 100);

// Set player's rank
api.setShopperRank(player, "gold");
```

---

## Events

InfiniteShops fires events that can be listened to:

### ShopBuyEvent

```java
@EventHandler
public void onShopBuy(ShopBuyEvent event) {
    Player player = event.getPlayer();
    ShopItem item = event.getItem();
    int amount = event.getAmount();
    double price = event.getPrice();
    
    // Cancel the purchase
    if (someCondition) {
        event.setCancelled(true);
        event.setCancelReason("Custom reason");
    }
    
    // Modify the price
    event.setPrice(price * 0.9); // 10% discount
}
```

### ShopSellEvent

```java
@EventHandler
public void onShopSell(ShopSellEvent event) {
    Player player = event.getPlayer();
    ItemStack item = event.getItem();
    int amount = event.getAmount();
    double price = event.getPrice();
    
    // Modify sell price
    event.setPrice(price * 1.1); // 10% bonus
}
```

### Available Events

| Event | Description | Cancellable |
|-------|-------------|-------------|
| `ShopBuyEvent` | Fired before a purchase | Yes |
| `ShopSellEvent` | Fired before a sale | Yes |
| `ShopOpenEvent` | Fired when shop opens | Yes |
| `BlackMarketBidEvent` | Fired when bid placed | Yes |
| `DailyShopResetEvent` | Fired on reset | No |
| `MultiplierActivateEvent` | Fired on multiplier add | Yes |
| `ShopperRankUpEvent` | Fired on rank up | No |

---

## Utilities

### Item Matching

```java
// Check if items match (ignoring amount)
boolean matches = api.itemMatches(item1, item2);

// Check if item is from a shop
boolean isShopItem = api.isShopItem(item);
```

### Configuration

```java
// Reload plugin configuration
api.reload();

// Get configuration value
Object value = api.getConfigValue("path.to.value");
```

---

## Example Plugin

```java
public class MyShopAddon extends JavaPlugin implements Listener {
    
    private InfiniteShopsAPI api;
    
    @Override
    public void onEnable() {
        api = InfiniteShopsAPI.getInstance();
        
        if (api == null) {
            getLogger().severe("InfiniteShops not found!");
            getServer().getPluginManager().disablePlugin(this);
            return;
        }
        
        getServer().getPluginManager().registerEvents(this, this);
        getLogger().info("MyShopAddon enabled!");
    }
    
    @EventHandler
    public void onBuy(ShopBuyEvent event) {
        Player player = event.getPlayer();
        
        // VIP players get 10% discount
        if (player.hasPermission("myserver.vip")) {
            double newPrice = event.getPrice() * 0.9;
            event.setPrice(newPrice);
            player.sendMessage("§a10% VIP discount applied!");
        }
    }
}
```

---

## Support

For API support and questions, contact us on Discord or open an issue on GitHub.

---

## Tips

1. **Check for null** - Always verify API instance exists before use
2. **Use events** - Listen to events rather than polling for changes
3. **Cache sparingly** - The API handles caching internally
4. **Handle async** - Some operations may be asynchronous
5. **Test thoroughly** - Verify integration on a test server first
