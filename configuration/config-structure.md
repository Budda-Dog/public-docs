# Config Structure

This guide explains the structure of TPM's configuration file (`config.json5`) and all available options.

## Overview

TPM uses a JSON configuration file (`config.json5`) that exports a configuration object. This file contains all settings for your bot's behavior, authentication, and flipping strategy.

## Basic Structure

```javascript
module.exports = {
    // Account Settings
    igns: ["account1", "account2"],

    // Discord Integration
    discordID: "your-backend-id",
    webhook: "your-discord-webhook-url",
    webhookFormat: "custom message format",
    sendAllFlips: "optional-test-webhook",

    // Authentication
    session: "your-coflnet-password",

    // Timing Settings
    delay: 250,
    waittime: 15,
    clickDelay: 100,

    // Flipping Configuration
    percentOfTarget: {...},
    listHours: {...},
    useCookie: true,
    autoCookie: "1d",
    relist: true,
    roundTo: 0,

    // Filters and Behaviors
    skip: {...},
    doNotRelist: {...},
    angryCoopPrevention: true,
    blockUselessMessages: true,
    pingOnUpdate: false,

    // Advanced Features
    visitFriend: "friend-username",
    autoRotate: {...},
    bedSpam: true
}
```

## Account Settings

### `igns` (Array)
Minecraft account usernames to use for flipping.

```javascript
igns: ["MainAccount", "AltAccount1", "AltAccount2"]
```

- Supports multiple accounts
- Each account will run as a separate bot instance
- Use account names (if token auth) or email addresses (if Microsoft auth)

### `discordID` (String)
Backend identifier from the TPM server. This is provided when you get access to TPM.

```javascript
discordID: "abc123xyz789"
```

## Discord Integration

### `webhook` (String)
Discord webhook URL for bot notifications.

```javascript
webhook: "https://discord.com/api/webhooks/..."
```

Notifications include:
- Purchases made
- Items sold
- Profits earned
- Bot startup/shutdown
- Errors and warnings

### `webhookFormat` (String)
Customizable message template with placeholders.

```javascript
webhookFormat: "Bought {itemName} for {price} coins!"
```

Available placeholders:
- `{itemName}` - Item name
- `{price}` - Purchase price
- `{target}` - Target sell price
- `{profit}` - Expected profit
- `{profitPercent}` - Profit percentage
- And more (12 total variables)

### `sendAllFlips` (String, Optional)
Additional webhook URL for testing or monitoring all flip opportunities (not just purchased items).

```javascript
sendAllFlips: "https://discord.com/api/webhooks/..."
```

## Authentication

### `session` (String)
Your Coflnet account password. Required for authenticating with SkyCofl.

```javascript
session: "your-coflnet-password"
```

**Important**: Keep this confidential! Never share your config file publicly with your session password in it.

## Timing Settings

### `delay` (Number)
Milliseconds between actions. Default: 250ms

```javascript
delay: 250
```

- Lower values = faster actions
- Too low may cause issues or flags
- Recommended range: 200-300ms

### `waittime` (Number)
Bed spam timing configuration in milliseconds. Default: 15ms

```javascript
waittime: 15
```

Used for bed spamming to claim flips quickly.

### `clickDelay` (Number)
Interval between bed spam clicks. Recommended: 100-125ms

```javascript
clickDelay: 100
```

### `bedSpam` (Boolean)
Enable/disable bed spamming for faster flip claiming.

```javascript
bedSpam: true
```

## Flipping Configuration

### `percentOfTarget` (Object)
Price ranges with percentage markups for listing items.

```javascript
TODO: FILL
```

### `listHours` (Object)
Listing duration by price tier.

```javascript
TODO: FILL
```

### `useCookie` (Boolean)
Enable/disable cookie usage for relisting.

```javascript
useCookie: true
```

### `autoCookie` (String)
Auto-purchase interval for cookies. Supports y/d/h units.

```javascript
autoCookie: "1d" 
```

### `roundTo` (Number)
Rounding digit for relist pricing.

```javascript
roundTo: 0  // No rounding
roundTo: 4  // Round to nearest 10,000
```

## Behavioral Filters

### `skip` (Object)
Conditions for bypassing confirmation screens.

# HIGHER BAN RISK
```javascript
skip: {
    profitThreshold: 5000000,  // Auto-buy if profit > 5M
    finderTypes: ["SNIPER", "USER"],
    cosmetics: true,            // Skip cosmetic items
    lowProfit: 1000000         // Skip if profit < 1M
}
```

### `doNotRelist` (Object)
Exclusion rules for specific items.

```javascript
doNotRelist: {
    items: ["Aspect of the Dragons", "Necron's Handle"],
    minProfit: 1000000,        // Don't relist if profit < 1M
    tags: ["VERY_SPECIAL"],    // Don't relist items with these tags
    finders: ["STONKS"]        // Don't relist from certain finders
}
```

### `angryCoopPrevention` (Boolean)
Blocks cooperative auction claims.

```javascript
angryCoopPrevention: true
```

Prevents claiming auctions from coop members (if applicable).

### `blockUselessMessages` (Boolean)
Suppress non-essential logs.

```javascript
blockUselessMessages: true
```

Reduces console spam by hiding minor messages.

### `pingOnUpdate` (Boolean)
Notifications for bot updates.

```javascript
pingOnUpdate: true
```

## Advanced Features

### `visitFriend` (String)
Island-based flipping capability.

```javascript
visitFriend: ""
```

Bot will visit friend's island for private flips or special access.

### `autoRotate` (Object)
Account-specific rest/flip scheduling.

```javascript
autoRotate: {
    "MainAccount": "r2:3f1",  // Rest 2 hours, flip 3 hours, friend visit 1 hour
    "AltAccount1": "r1:2f2"   // Custom schedule for each account
}
```

Schedule format: `"r[hours]:f[hours]f[hours]"`
- `r` = rest/offline time
- `f` = flip time
- Can chain multiple periods

## Next Steps

- Learn about [Filters and Settings](filters-and-settings.md) in detail
- Understand [Cofl Commands](cofl-commands.md) for in-game adjustments
- Read about [Loading Configs](../guides/loading-configs.md)
