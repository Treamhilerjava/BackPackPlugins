<div align="center">

# 🎒 BackpackPlugin

**Tiered backpacks with upgrades, NPC shop, and unlimited custom types**

[![Modrinth](https://img.shields.io/modrinth/v/backpackplugin?label=Modrinth&logo=modrinth&color=1bd96a)](https://modrinth.com/plugin/backpackplugin)
[![Discord](https://img.shields.io/discord/1234567890?label=Discord&logo=discord&color=5865F2)](https://discord.gg/tFXhkPVpxG)
[![Java](https://img.shields.io/badge/Java-21-orange?logo=openjdk)](https://adoptium.net/)
[![Paper](https://img.shields.io/badge/Paper-1.21.x-white?logo=spigotmc)](https://papermc.io/)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

</div>

---

A fully configurable tiered backpack plugin for Paper 1.21. Players purchase and upgrade backpacks through 6 built-in tiers, each with a unique custom head, auto-pickup, sort button, armor bonus, and NPC shop. Add unlimited custom types with a single command — no resource pack required.

---

## ✨ Features

- **6 built-in tiers** — Worn Satchel → Leather → Iron → Gold → Diamond → Ender
- **Unlimited custom types** — add any backpack via `backpacks.yml` or the in-game 9-step wizard
- **Custom player head** per tier — no resource pack needed
- **Equippable in chestplate slot** — grants armor points; Shift+Right-click to equip/unequip
- Works in **mainhand, offhand, and chestplate slot**
- **Auto-pickup** toggle — items go directly into the bag
- **Sort button** — sorts contents alphabetically by item type
- **Rename system** — configurable XP cost, supports colour codes
- **FancyNPCs merchant** — buy and upgrade from in-world NPCs
- **Upgrade system** — storage rows, auto-pickup unlock, armor points — each with its own cost curve
- **Paginated GUI** — up to 54 rows of storage across 9 pages
- **NBT storage** — contents saved on the item itself; survive restarts, drops, and transfers
- **Death behavior** — configurable: `DROP`, `KEEP`, or `DELETE`
- **ItemsAdder support** — use any custom item as the visual; falls back to skull if unavailable
- **Bedrock support** via Geyser — `/bp` opens your equipped backpack

---

## 🎒 Built-in Tiers

| Tier | Initial Rows | Max Rows | Price |
|---|---|---|---|
| Worn Satchel | 1 | 3 | $500 |
| Leather Backpack | 2 | 5 | $2,000 |
| Iron Backpack | 3 | 8 | $5,000 |
| Gold Backpack | 4 | 12 | $12,000 |
| Diamond Backpack | 5 | 18 | $30,000 |
| Ender Backpack | 6 | 24 | $75,000 |

> All values are configurable in `backpacks.yml`.

---

## 📋 Requirements

| Requirement | Version | Notes |
|---|---|---|
| Paper | 1.21.x | Spigot not supported |
| Java | 21+ | |
| Vault | Any | + an economy plugin |
| FancyNPCs | 2.9+ | Optional — for merchant NPCs |
| ItemsAdder | 3.6+ | Optional — for custom visuals |
| Geyser | Any | Optional — Bedrock support |

---

## 🚀 Installation

1. Drop `BackpackPlugin.jar` into your `plugins/` folder
2. Ensure **Vault** + an economy plugin are installed
3. Restart — `config.yml` and `backpacks.yml` are generated automatically
4. Optionally install **FancyNPCs** and/or **ItemsAdder**
5. Run `/backpack reload` after any config changes

---

## 🎮 Usage

### Opening a Backpack

| Method | Java | Bedrock |
|---|---|---|
| Mainhand | Right-click | Long-press |
| Offhand | Right-click | Long-press |
| Equipped (chest slot) | `/bp` | `/bp` |

### Equipping
Hold the backpack → **Shift + Right-click** to equip to chestplate slot. Repeat to unequip.

### GUI Controls

| Button | Function |
|---|---|
| Sort | Alphabetically sorts contents |
| Auto-Pickup | Toggles ON/OFF |
| Rename | Costs XP levels (configurable) |
| Prev / Next | Navigate storage pages |

---

## 🛒 NPC Shop

```
/backpack spawnnpc <name>
```

Spawns a merchant NPC. Players use the **Buy** tab to purchase tiers and the **Upgrade** tab to upgrade their existing backpack. The shop auto-populates from `backpacks.yml` — no extra setup after adding new types.

---

## ➕ Adding Custom Backpacks

**In-game wizard (recommended):**
```
/backpack create mythic_backpack
```
A 9-step chat wizard prompts for display name, skull texture, ItemsAdder ID, initial rows, max rows, armor base, and upgrade costs. Clickable `[Give to yourself]` and `[Edit fields]` buttons appear on completion.

**Direct YAML edit:**
```yaml
# backpacks.yml
backpacks:
  mythic_backpack:
    display:        "&d&lMythic Backpack"
    price:          150000.0
    skull_texture:  "eyJ..."   # Base64 from minecraft-heads.com
    itemsadder_id:  ""         # e.g. mynamespace:my_item — leave blank for skull
    initial_rows:   6
    max_rows:       36
    armor_base:     5
    upgrades:
      storage:
        enabled:           true
        max_purchases:     30
        rows_per_purchase: 1
        base_cost:         20000.0
        cost_multiplier:   1.6
      autopickup:
        enabled: true
        cost:    40000.0
      armor:
        enabled:             true
        max_purchases:       8
        points_per_purchase: 1
        base_cost:           15000.0
        cost_multiplier:     1.6
```
Run `/backpack reload` to hot-load the new type.

---

## 💻 Commands & Permissions

| Command | Permission | Description |
|---|---|---|
| `/bp` | `backpack.use` | Open your equipped backpack |
| `/backpack shop` | `backpack.use` | Open the NPC shop manually |
| `/backpack give <player> <id>` | `backpack.admin` | Give a backpack to a player |
| `/backpack create <id>` | `backpack.admin` | Start the creation wizard |
| `/backpack cancel` | `backpack.admin` | Abort an active wizard |
| `/backpack bpedit <id> <field> <value>` | `backpack.admin` | Edit a backpack type live |
| `/backpack bpdelete <id>` | `backpack.admin` | Delete a backpack type |
| `/backpack list` | `backpack.admin` | List all loaded backpack IDs |
| `/backpack reload` | `backpack.admin` | Reload config.yml and backpacks.yml |
| `/backpack spawnnpc <name>` | `backpack.admin` | Spawn a merchant NPC |
| `/backpack removenpc <name>` | `backpack.admin` | Remove a merchant NPC |

| Permission | Default |
|---|---|
| `backpack.use` | Everyone |
| `backpack.autopickup` | Everyone |
| `backpack.bypass.blacklist` | false |
| `backpack.admin` | OP |

---

## 🏷️ Lore Placeholders

| Placeholder | Value |
|---|---|
| `{name}` | Custom name or default display name |
| `{type}` | Original type ID |
| `{slots_used}` / `{slots_total}` | Storage fill |
| `{rows}` | Current row count |
| `{autopickup}` | On / Off |
| `{level}` / `{max_level}` | Upgrade progress |
| `{armor}` | Current armor points |

---

## 📁 Project Structure

```
src/main/java/org/backpack/
├── BackpackPlugin.java          # Plugin entry point
├── BackpackRegistry.java        # Loads and manages backpacks.yml
├── BackpackItem.java            # Item creation, NBT, equip/unequip
├── BackpackManager.java         # Player data and backpack resolution
├── BackpackGUI.java             # Storage GUI and control buttons
├── BackpackListener.java        # Interact, equip, autopickup, rename events
├── BackpackCommand.java         # /backpack command handler
├── BackpackCreationWizard.java  # In-game 9-step creation wizard
├── BpCommand.java               # /bp command (Bedrock-friendly open)
├── NpcShopGUI.java              # Buy and Upgrade shop GUI
├── NpcShopListener.java         # Shop click handling and transactions
├── UpgradeData.java             # Per-player upgrade state model
├── ContentsSerializer.java      # NBT contents serialization
└── Sounds.java                  # Sound helper
```

---

## 📜 Changelog

See [CHANGELOG.md](CHANGELOG.md)

---

<div align="center">

💬 **[Discord](https://discord.gg/tFXhkPVpxG)** · 🔗 **[Modrinth](https://modrinth.com/user/Treamhiler)** · 🐙 **[GitHub](https://github.com/Treamhilerjava)**

Made by **Treamhiler**

</div>
