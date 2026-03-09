# 🎒 BackpackPlugin

A semi-MMO tiered backpack plugin for Paper 1.21 servers. Players can earn, craft, and upgrade backpacks with unique custom head appearances, auto-pickup, sorting, and full Bedrock/Geyser support.

---

## 📦 Installation

1. Drop `BackpackPlugin.jar` into your server's `plugins/` folder
2. Restart the server
3. Edit `plugins/BackpackPlugin/config.yml` to configure your tiers, mob drops, and messages
4. Give yourself a backpack to test: `/backpack give <player> worn_satchel`

---

## 🎒 Backpack Tiers

| Tier | Display | Slots | How to Obtain |
|---|---|---|---|
| `worn_satchel` | §7Worn Satchel | 18 | Mob drop (Zombie, Skeleton, Creeper) / Craft |
| `leather_backpack` | §aLeather Backpack | 27 | Craft (upgrade from Worn Satchel) / Mob drop |
| `iron_backpack` | §fIron Backpack | 36 | Craft (upgrade from Leather) / Mob drop |
| `gold_backpack` | §6Gold Backpack | 45 | Craft (upgrade from Iron) / Mob drop |
| `diamond_backpack` | §bDiamond Backpack | 54 | Craft (upgrade from Gold) / Boss drop |

Each tier is represented by a **custom player head** — no resource pack required. Works on both Java and Bedrock via Geyser.

---

## 🎮 How to Use

### Opening a Backpack
| Method | Java | Bedrock |
|---|---|---|
| Hold in hand | Right-click | Long-press (Geyser translates automatically) |
| From offhand | Right-click | Long-press |
| From chest slot | `/bp` | `/bp` |
| Keybind | Bind `/bp` to **B key** in any macro mod | N/A |

### Equipping to Chest Slot
- Hold the backpack in your **mainhand**
- **Shift + Right-click** to equip it to your chestplate slot
- **Shift + Right-click** again (while empty-handed or holding another item) to unequip
- Wearing a backpack gives **+2 armor points**

### Inside the Backpack GUI
The bottom row of the GUI contains two control buttons:

| Slot | Button | Function |
|---|---|---|
| Bottom-left | 🔽 Sort | Sorts all contents alphabetically by item type |
| Bottom-right | Auto-Pickup | Toggles auto-pickup ON/OFF for this backpack |

### Auto-Pickup
When enabled, items you walk over are automatically pulled into the backpack instead of your main inventory. Toggle it with the button inside the GUI or it will reflect the server default on new backpacks.

---

## 🛠️ Commands

### `/bp`
Open your equipped backpack. Checks in this priority order:
1. Chestplate slot
2. Offhand
3. Mainhand

**Permission:** `backpack.use` (default: all players)
**Bedrock tip:** Bedrock players should use `/bp` as their primary way to open backpacks.

### `/backpack give <player> <tier>`
Give a backpack to a player.

```
/backpack give Treamhiler diamond_backpack
```

### `/backpack reload`
Reload `config.yml` without restarting the server.

**Permission for admin commands:** `backpack.admin` (default: OP)

---

## ⚙️ Configuration

File: `plugins/BackpackPlugin/config.yml`

### Death Behavior
```yaml
death:
  behavior: DROP   # DROP | KEEP | DELETE
```
- `DROP` — backpack item drops at death location (contents preserved inside)
- `KEEP` — player keeps the backpack on death
- `DELETE` — backpack and all contents are lost

### Armor Points
```yaml
armor_points: 2   # points added when worn in chestplate slot
```

### Auto-Pickup Default
```yaml
autopickup:
  default: false   # whether new backpacks have auto-pickup on or off
```

### Adding / Editing Tiers
```yaml
tiers:
  diamond_backpack:
    display: "&bDiamond Backpack"   # color code + name
    rows: 6                          # 1-6 rows (x9 slots each)
    skull_texture: "eyJ..."          # Base64 from minecraft-heads.com
    mob_drops:
      WITHER: 0.50                   # 50% chance on Wither kill
      ELDER_GUARDIAN: 0.20           # 20% chance on Elder Guardian kill
    recipe:
      enabled: true
      shape:
        - "DSD"
        - "DBD"
        - "DSD"
      ingredients:
        D: DIAMOND
        S: STRING
        B: gold_backpack             # tier key = requires that backpack as ingredient
```

#### Finding Custom Head Textures
1. Go to [minecraft-heads.com](https://minecraft-heads.com)
2. Search for a backpack head
3. Copy the **Value** field (the long Base64 string)
4. Paste it into `skull_texture` in config
5. Run `/backpack reload`

---

## 🪛 Crafting Recipes

All recipes use the shape defined in `config.yml`. Upgrade recipes require the previous tier backpack as a center ingredient.

**Worn Satchel** (base recipe):
```
S L S
L L L
S L S
(L=Leather, S=String)
```

**Leather → Iron → Gold → Diamond** all follow the same pattern — surround the previous backpack with the new material + string in corners.

---

## 🔧 Requirements

- Paper / Spigot 1.21.x
- Java 21+
- Geyser (optional, for Bedrock support — works automatically)

---

## 🔑 Permissions

| Permission | Default | Description |
|---|---|---|
| `backpack.use` | Everyone | Open and use backpacks |
| `backpack.autopickup` | Everyone | Use auto-pickup feature |
| `backpack.admin` | OP | `/backpack give` and `/backpack reload` |

---

## 🙏 Credits

Developed by **Treamhiler**
Support: discord.gg/tFXhkPVpxG
