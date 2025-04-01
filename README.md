### 📝 Docs
- Visit : https://connector.mintlify.app

##

## Features 🌟

- Fetch Discord roles for players
- Check if players have specific roles
- Get Discord usernames and avatars
- Rate limiting to prevent Rate Limiting
- Caching system for better performance

##

## Install 💻

1. Download the latest release or clone this repository
2. Place the `connector_discord` folder in your server's `resources` directory
3. Add `ensure connector_discord` to your server.cfg
4. Configure the `config.lua` file with your Discord bot token and server ID

##

## Config 📝

Edit `config.lua` with your settings:

```
Config = {
    Token = 'DISCORD_BOT_TOKEN',  -- Put Bot Token Here
    Guild = 'DISCORD_SERVER_ID',  -- Put Server ID Here
    
    RateLimit = {
        Enabled = true,     -- Enable rate limiting
        Requests = 30,      -- Max requests
        Interval = 60       -- Per X seconds
    },
    
    Cache = {
        Duration = 3600,    -- Cache duration in seconds ( this is 1 hour )
        Enabled = true      -- Enable Or Disable Caching ( true or false )
    }
}
```

##

# Usage / Exports 🔨

-- Get all Discord roles for a player
local roles = exports.connector_discord:GetDiscordRoles(playerId)

-- Check if player has a specific role (can check for singular or multiple)
local hasRole = exports.connector_discord:HasDiscordRole(playerId, roleId)
local hasAnyRole = exports.connector_discord:HasDiscordRole(playerId, {roleId1, roleId2, roleId3})

-- Get players Discord username
local username = exports.connector_discord:GetDiscordName(playerId)

-- Get players Discord avatar URL
local avatar = exports.connector_discord:GetDiscordAvatar(playerId)

-- Get players Discord ID
local discordId = exports.connector_discord:GetDiscordId(playerId)

-- Get all Discord data for a player
local discordData = exports.connector_discord:GetDiscordUser(playerId)
-- Returns: { name = string, avatar = string, roles = table }

##

# Implementation Example 📁

```
-- example role check command
RegisterCommand('checkstaff', function(source)
    local playerId = source
    if exports.connector_discord:HasDiscordRole(playerId, 'STAFF_ROLE_ID') then
        TriggerClientEvent('chat:addMessage', playerId, {
            color = {255, 0, 0},
            args = {'SYSTEM', 'You are a staff member!'}
        })
    else
        TriggerClientEvent('chat:addMessage', playerId, {
            color = {255, 0, 0},
            args = {'SYSTEM', 'You are not staff!'}
        })
    end
end)

-- Display Discord info when player joins
RegisterNetEvent('playerJoining', function()
    local playerId = source
    local discordName = exports.connector_discord:GetDiscordName(playerId)
    local discordAvatar = exports.connector_discord:GetDiscordAvatar(playerId)
    
    print(('Player %s joined - Discord: %s'):format(GetPlayerName(playerId), discordName)
    
    if discordAvatar then
    end
end)
```

##

# Setup Discord Bot 🤖

- Go to [Discord Developer Portal](https://discord.com/developers/applications) and click `New Application`
- Set the bot name and click the TOS checkbox then press `create`, Now click `bot` scroll down to Privileged Gateway Intents
- Make sure discord bot has all 3 intents ( Presence Intent, Server Members Intent, Message Content Intent )
- Below you will see `Default Install Settings` click scopes and make sure `bot` & `applications.commands` are selected
- And then for permissions set it to `Administrator` after this click `OAuth2` click `bot` & `applications.commands` then copy the URL
- After copying the URL paste it in your browser or in your discord and click it, invite the bot to your server, Now go back to developer portal and reset bot `token`

##

# Support 🔗

- Need support or ran into a error, Join my [Discord Server](https://discord.gg/obfuscate)
- Feel like you could improve the script, well then please submit a pull request and we will review **ASAP**

##

<p align="center"> <img src="https://badges.frapsoft.com/os/v3/open-source.svg?v=103" alt="Open Source"> <img src="https://img.shields.io/badge/Lua-2C2D72?style=flat&logo=lua&logoColor=white"> <img src="https://img.shields.io/badge/FiveM-compatible-green"> </p>
