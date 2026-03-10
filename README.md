<div align="center">

# 🎒 BackpackPlugin

**A fully configurable tiered backpack plugin for Paper 1.21**

[![Modrinth](https://img.shields.io/badge/Modrinth-BackpackPlugin-00AF5C?style=for-the-badge&logo=modrinth)](https://modrinth.com/user/Treamhiler)
[![Discord](https://img.shields.io/badge/Discord-Support-5865F2?style=for-the-badge&logo=discord)](https://discord.gg/tFXhkPVpxG)
[![Paper](https://img.shields.io/badge/Paper-1.21.x-F96854?style=for-the-badge)](https://papermc.io)
[![Java](https://img.shields.io/badge/Java-21+-orange?style=for-the-badge&logo=openjdk)](https://adoptium.net)

*6 built-in tiers · Unlimited custom types · FancyNPCs shop · NPC merchant · ItemsAdder support · No resource pack required*

</div>

---

## ✨ Features

| Feature | Details |
|---|---|
| 🎒 Tiered backpacks | 6 built-in tiers from Worn Satchel to Ender Backpack |
| ♾️ Unlimited custom types | Add any backpack via `backpacks.yml` or `/backpack create` wizard |
| 🪄 In-game wizard | Step-by-step chat wizard to create new types without editing files |
| 🗄️ Paginated GUI | Up to 54 rows of storage across 9 pages |
| 🧲 Auto-pickup | Toggle per backpack — items go straight into the bag |
| 🛍️ NPC Shop | FancyNPCs merchant for buying and upgrading backpacks |
| 🔼 Upgrade system | Storage rows, auto-pickup unlock, and armor points per tier |
| 🛡️ Chestplate equip | Wear a backpack for bonus armor — works in mainhand/offhand/chest slot |
| ✏️ Rename system | Rename with colour codes, costs configurable XP levels |
| 📦 ItemsAdder support | Use custom items as the backpack visual |
| 💀 Death behavior | Configurable: `DROP`, `KEEP`, or `DELETE` |
| 🪨 Bedrock support | Full Geyser compatibility via `/bp` command |

---

## 📋 Requirements

- [Paper](https://papermc.io) 1.21.x
- Java 21+
- [Vault](https://www.spigotmc.org/resources/vault.34315/) + any economy plugin
- [FancyNPCs](https://modrinth.com/plugin/fancynpcs) 2.9+
- [ItemsAdder](https://www.spigotmc.org/resources/itemsadder.73355/) 3.6+ *(optional)*
- [Geyser](https://geysermc.org) *(optional, Bedrock support)*

---

## 🚀 Installation

1. Drop `BackpackPlugin.jar` into your `plugins/` folder
2. Install Vault, FancyNPCs, and an economy plugin
3. Start the server — `config.yml` and `backpacks.yml` are auto-generated
4. Edit `plugins/BackpackPlugin/backpacks.yml` to customise tiers
5. Run `/backpack reload`

---

## 🎒 Built-in Tiers

| Tier | Starting Rows | Max Rows | Shop Price | Armor Base |
|---|---|---|---|---|
| Worn Satchel | 1 | 3 | $500 | 1 |
| Leather Backpack | 2 | 5 | $2,000 | 1 |
| Iron Backpack | 3 | 8 | $5,000 | 2 |
| Gold Backpack | 4 | 12 | $12,000 | 2 |
| Diamond Backpack | 5 | 18 | $30,000 | 3 |
| Ender Backpack | 6 | 24 | $75,000 | 4 |

> All values are fully configurable in `backpacks.yml`.

---

## 🛠️ Commands

| Command | Permission | Description |
|---|---|---|
| `/bp` | `backpack.use` | Open your backpack |
| `/backpack shop` | `backpack.use` | Open the NPC shop manually |
| `/backpack give <player> <id>` | `backpack.admin` | Give a backpack to a player |
| `/backpack create <id>` | `backpack.admin` | Start in-game creation wizard |
| `/backpack bpedit <id> <field> <value>` | `backpack.admin` | Edit a backpack type live |
| `/backpack bpdelete <id>` | `backpack.admin` | Delete a backpack type |
| `/backpack list` | `backpack.admin` | List all loaded backpack IDs |
| `/backpack reload` | `backpack.admin` | Reload configs |
| `/backpack edit <player> <id> <field> <value>` | `backpack.admin` | Edit a player's upgrades |
| `/backpack spawnnpc <n>` | `backpack.admin` | Spawn a merchant NPC |
| `/backpack removenpc <n>` | `backpack.admin` | Remove a merchant NPC |

---

## 🔑 Permissions

| Permission | Default | Description |
|---|---|---|
| `backpack.use` | Everyone | Open and use backpacks |
| `backpack.autopickup` | Everyone | Use auto-pickup feature |
| `backpack.bypass.blacklist` | `false` | Bypass autopickup item blacklist |
| `backpack.admin` | OP | All admin commands |

---

## ➕ Adding Custom Backpacks

### Option 1 — In-game wizard
```
/backpack create mythic_backpack
```
Answer 9 chat prompts. Clickable buttons appear at the end to instantly give yourself the new backpack or edit any field.

### Option 2 — Edit `backpacks.yml` directly

```yaml
backpacks:
  mythic_backpack:
    display:        "&d&lMythic Backpack"
    price:          150000.0
    skull_texture:  "eyJ..."      # Base64 from minecraft-heads.com
    itemsadder_id:  ""            # e.g. mypack:mythic_bag
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

Then run `/backpack reload`. The new type appears in the NPC shop instantly.

---

## ⚙️ Configuration Files

### `config.yml` — GUI, sounds, messages, lore template

```yaml
death:
  behavior: DROP    # DROP | KEEP | DELETE

autopickup:
  default: false
  blacklist: []

lore:
  - " &7Type&f: {type}"
  - " &7Storage&f: &a{slots_used}&7/&f{slots_total} &7slots &8({rows} rows)"
  - " &7Level&f: {level}&7/&f{max_level}  &7Armor&f: +{armor}"
  - " &7Auto-pickup&f: {autopickup}"
```

**Lore placeholders:** `{name}` `{type}` `{slots_used}` `{slots_total}` `{rows}` `{autopickup}` `{level}` `{max_level}` `{armor}`

### `backpacks.yml` — All backpack type definitions

This is the only file you need to edit to add, remove, or change backpack types. See the section above for a full example.

---

## 📁 Project Structure

```
src/main/java/org/backpack/
├── BackpackPlugin.java          # Main plugin class
├── BackpackRegistry.java        # Loads & manages backpacks.yml
├── BackpackCreationWizard.java  # In-game chat wizard
├── BackpackCommand.java         # All /backpack subcommands
├── BackpackItem.java            # Item creation & PDC storage
├── BackpackGUI.java             # Paginated inventory GUI
├── BackpackManager.java         # Open/close/save logic
├── BackpackListener.java        # Inventory & player events
├── NpcManager.java              # FancyNPCs merchant creation
├── NpcShopGUI.java              # Shop GUI (buy + upgrade pages)
├── NpcShopListener.java         # Shop click handling
├── UpgradeData.java             # Upgrade state record
├── ContentsSerializer.java      # Item serialization to NBT
├── Sounds.java                  # Sound helpers
└── BpCommand.java               # /bp shortcut command

src/main/resources/
├── plugin.yml
├── config.yml
└── backpacks.yml
```

---

## 🙏 Credits

Developed by **Treamhiler**

[modrinth.com/user/Treamhiler](https://modrinth.com/user/Treamhiler) • [discord.gg/tFXhkPVpxG](https://discord.gg/tFXhkPVpxG) • [github.com/Treamhilerjava](https://github.com/Treamhilerjava)
