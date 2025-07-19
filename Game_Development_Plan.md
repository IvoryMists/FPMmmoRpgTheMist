# FPMMORPG Game Development Plan

## 1. Executive Summary
- **Genre:** Online Action RPG inspired by “The King’s Avatar”
- **Target Platforms:** PC (Windows, macOS), Mobile Companion App (iOS, Android)
- **Core Pillars:**
  - Deep class & skill system: 6 main classes, 4 subclasses each
  - Custom weapon crafting: Silver weapon aesthetic
  - Equipment-driven character stats
  - Massive world bosses, dungeons/raids
  - Single super-server per continent
  - Robust social features: chat, friends, guilds
  - Companion app chat integration

## 2. Game Concept
- **Playable Characters:** Humans only; full customization of appearance
- **Classes & Subclasses:**
  1. Warrior: Knight, Berserker, Gladiator, Sentinel
  2. Mage: Elementalist, Necromancer, Chronomancer, Arcanist
  3. Rogue: Assassin, Ranger, Trickster, Shadowblade
  4. Cleric: Healer, Paladin, Inquisitor, Templar
  5. Engineer: Gunsmith, Tinkerer, Artificer, Mechanist
  6. Hybrid: Spellblade, Battlemage, Spellblade, Shadowcaster
- **Skills:** 
  - Characters earn **180** skill points by level 60.
  - Additional **60** skill points from quests and world boss drops.
  - Skills can be leveled using skill points.

## 3. Core Gameplay Features

### 3.1 Character Creation
- Human-only race.
- Sliders for facial features, body, hair, skin tone.
- Choose initial appearance; unlock cosmetics via gameplay.

### 3.2 Combat & Skill System
- Active skill bar: 8 slots.
- Passive skill traits.
- Skill point allocation at character menu.
- Subclass unlock at level 20; allows mixing skills across classes pre-20.

### 3.3 Equipment & Weapons
- **Base Stats:** Starting stats fixed; increase with level via fixed growth.
- **Equipment Stats:** Primary source of character power.
- **Weapon Crafting:** 
  - “Silver Weapon” design templates.
  - Resource gathering & forging minigame.
  - Legendary variants from world bosses.

### 3.4 World Content
- **Open World:** Four continents, each with unique biomes.
- **Dungeons & Raids:** 5-person & 20-person instanced.
- **World Bosses:** Scheduled spawns; drop high-tier loot.

## 4. Social & Networking

### 4.1 Chat System
- In-game chat channels: Global, Zone, Party, Raid, Guild.
- Direct messages.
- Companion app chat mirrors in-game channels & DMs.

### 4.2 Friends & Guilds
- Friend list with presence indicators.
- Guild system: creation, ranking, bank, guild skills.

### 4.3 Authentication & Account Linking
- **USB Token Linking:** Allow users to link their USB token to their in-game and companion-app accounts.
- **Cross-Platform Sync:** The same hardware token credentials grant access to both the game client and companion chat app.

## 5. Technical Architecture

### 5.1 Server Structure
- **Single super-server per continent** to maximize community.
- **Regional shard** architecture for data distribution.
- **Authoritative master server** for login & matchmaking.
- **Microservices**: Chat, Character, Combat, Economy, Crafting.

### 5.2 Database & Persistence
- **Relational DB** for core data.
- **NoSQL** for chat logs & analytics.
- **Redis** for real-time session data.

### 5.3 USB Stick Authentication
- **Hardware Token Login:** Players can authenticate using a USB security token (“USB stick”) that holds a unique private key and certificate tied to their account.
- **Integration Flow:**
  1. **Provisioning:** On account creation, generate a public/private key pair; program the private key and user certificate onto the USB token.
  2. **Login Process:** At client launch, the game and companion app detect the USB token via OS APIs. The client challenges the token to sign a server-provided nonce.
  3. **Server Validation:** The server validates the signed nonce against the stored public key. Upon success, the server issues a session token.
- **Companion App Integration:**
  - The mobile/desktop companion mirrors the same USB-auth flow when running on platforms with USB support (desktop), or can allow QR-code or NFC equivalents on mobile.
  - On desktop companion app, use platform-specific USB libraries to prompt the user to insert the token, then perform the same challenge/response.
  - On mobile, register the hardware ID from the primary USB-authenticated login for out-of-band chat access.
- **Security Considerations:**
  - Implement secure PIN-protection on the USB token to prevent unauthorized use.
  - Fallback 2FA via email or authenticator app if the token is lost.

## 6. Progression & Economy
- **Level Cap:** 60
- **Skill Points:** 240 total (180 via leveling, 60 via content).
- **Currency:** Gold, Crafting Resource, Gems.
- **Marketplace:** Auction house & player shops.

## 7. Development Roadmap

| Phase           | Duration | Milestones                                      |
|-----------------|----------|-------------------------------------------------|
| Pre-production  | 2 mo     | Game design document, tech prototyping          |
| Prototype       | 3 mo     | Basic combat, UI, server setup                 |
| Vertical Slice  | 4 mo     | 1 continent, 2 classes, dungeon, chat           |
| Alpha           | 6 mo     | All classes, subclass system, crafting, raids   |
| Beta            | 3 mo     | Stress test, localization, balancing            |
| Launch          | -        | Global release                                  |

## 8. Appendix
- **Art Style References:** Silver weapons, UI mockups.
- **Network Diagrams:** Super-server topology.
- **UI Wireframes:** Character creation, skill tree.

---

*Prepared for the FPMMORPG team. Please share feedback and questions!*
