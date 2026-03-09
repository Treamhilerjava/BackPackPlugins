# 🎒 BackpackPlugin

A semi-MMO tiered backpack plugin for Paper 1.21 servers. Players can earn, craft, and upgrade backpacks through 5 tiers — each with a unique custom head appearance, auto-pickup, inventory sorting, and full Bedrock/Geyser support. No resource pack required.

> 🔗 **More projects by Treamhiler:** [modrinth.com/user/Treamhiler](https://modrinth.com/user/Treamhiler)
> 💬 **Support & Downloads:** [discord.gg/tFXhkPVpxG](https://discord.gg/tFXhkPVpxG)
> 🐙 **GitHub:** [github.com/Treamhilerjava](https://github.com/Treamhilerjava)

---

## ✨ Features

- 5 backpack tiers — Worn Satchel → Leather → Iron → Gold → Diamond
- Custom player head appearance per tier — no resource pack needed
- Equippable in the chestplate slot (+2 armor points)
- Works in mainhand, offhand, and chestplate slot
- Auto-pickup toggle per backpack
- Sort button inside the GUI
- Upgrade crafting recipes (each tier requires the previous as an ingredient)
- Mob drop system with configurable per-mob per-tier chances
- Boost state persists across restarts — contents saved in NBT on the item itself
- Full Bedrock support via Geyser (long-press = right-click, `/bp` command)
- Configurable death behavior: DROP, KEEP, or DELETE

---

## 🎒 Backpack Tiers

| Tier | Slots | How to Obtain |
|---|---|---|
| Worn Satchel | 18 | Craft / Zombie, Skeleton, Creeper drop |
| Leather Backpack | 27 | Craft (upgrade) / Pillager drop |
| Iron Backpack | 36 | Craft (upgrade) / Iron Golem, Vindicator drop |
| Gold Backpack | 45 | Craft (upgrade) / Piglin Brute, Wither Skeleton drop |
| Diamond Backpack | 54 | Craft (upgrade) / Ender Dragon, Wither, Elder Guardian drop |

---

## 🎮 How to Use

### Opening a Backpack

| Method | Java | Bedrock |
|---|---|---|
| Hold in mainhand | Right-click | Long-press |
| Hold in offhand | Right-click | Long-press |
| Worn in chest slot | `/bp` | `/bp` |
| Keybind | Bind `/bp` to **B key** | N/A |

### Equipping to Chest Slot
- Hold the backpack in your **mainhand**
- **Shift + Right-click** to equip it to your chestplate slot
- **Shift + Right-click** again to unequip it
- Wearing a backpack grants **+2 armor points**

### Inside the GUI
The bottom control row has two buttons:

| Button | Function |
|---|---|
| Sort (bottom-left) | Sorts contents alphabetically by item type |
| Auto-Pickup (bottom-right) | Toggles auto-pickup ON/OFF for this backpack |

When auto-pickup is ON, items you walk over go directly into the backpack instead of your main inventory.

---

## 🛠️ Commands

| Command | Permission | Description |
|---|---|---|
| `/bp` | `backpack.use` | Open your backpack (chest → offhand → mainhand priority) |
| `/backpack give <player> <tier>` | `backpack.admin` | Give a backpack to a player |
| `/backpack reload` | `backpack.admin` | Reload config without restarting |

**Bedrock tip:** `/bp` is the primary way for Bedrock players to open their backpack.

---

## ⚙️ Configuration

File: `plugins/BackpackPlugin/config.yml`

```yaml
# DROP | KEEP | DELETE
death:
  behavior: DROP

# Armor points when worn in chestplate slot
armor_points: 2

# Default auto-pickup state for new backpacks
autopickup:
  default: false

tiers:
  diamond_backpack:
    display: "&bDiamond Backpack"
    rows: 6
    skull_texture: "eyJ..."      # Base64 from minecraft-heads.com
    mob_drops:
      WITHER: 0.50
      ELDER_GUARDIAN: 0.20
    recipe:
      enabled: true
      shape:
        - "DSD"
        - "DBD"
        - "DSD"
      ingredients:
        D: DIAMOND
        S: STRING
        B: gold_backpack         # requires previous tier as ingredient
```

### Finding Custom Head Textures
1. Go to [minecraft-heads.com](https://minecraft-heads.com) and search for a backpack skin
2. Copy the **Value** field (the long Base64 string)
3. Paste it into `skull_texture` in config
4. Run `/backpack reload`

---

## 🔑 Permissions

| Permission | Default | Description |
|---|---|---|
| `backpack.use` | Everyone | Open and use backpacks |
| `backpack.autopickup` | Everyone | Use auto-pickup feature |
| `backpack.admin` | OP | Admin commands |

---

## 🔧 Requirements

- Paper / Spigot 1.21.x
- Java 21+
- Geyser (optional, for Bedrock support — works automatically)

---

## 🙏 Credits

Developed by **Treamhiler**
[modrinth.com/user/Treamhiler](https://modrinth.com/user/Treamhiler) • [discord.gg/tFXhkPVpxG](https://discord.gg/tFXhkPVpxG) • [github.com/Treamhilerjava](https://github.com/Treamhilerjava)
