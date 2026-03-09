# 🚀 SellBoost

A premium Bukkit/Paper plugin that integrates with **EconomyShopGUI** to trigger randomized sell price multiplier events at configurable intervals. When a boost is active, randomly selected shop items get their own multiplier — displayed live on the actionbar.

---

## 📦 Installation

1. Drop `SellBoost.jar` into your server's `plugins/` folder
2. Ensure **EconomyShopGUI** (free or premium) is already installed
3. Restart the server
4. Edit `plugins/SellBoost/config.yml` with your shop item paths
5. Run `/sellboost reload`

---

## ⚙️ Configuration

File: `plugins/SellBoost/config.yml`

```yaml
# ================================
# SellBoost v2.0.0 by Treamhiler
# ================================

# MULTIPLE = multiple items boosted at once, each with its own multiplier
# SINGLE   = one item boosted at a time
mode:
  type: MULTIPLE
  multiple:
    count: 3              # how many items get boosted at once
    no_repeat_last: true  # prevents same items being picked back to back

# How often a boost fires automatically
rotation:
  unit: MINUTES           # HOURS | MINUTES | SECONDS
  value: 60

# How long each boost lasts
boost:
  duration:
    unit: MINUTES
    value: 15

# Multiplier range — random value picked between min and max using step increments
# Example with step 0.5: possible values are 2.0, 2.5, 3.0, 3.5, 4.0
multiplier:
  min: 2.0
  max: 4.0
  step: 0.5

# Autosave boost state — allows boost to resume after a server restart
autosave:
  enabled: true
  interval_ticks: 200

# Items eligible for boosting
# path   = EconomyShopGUI item path (ShopName.pageX.items.SLOT)
# display = name shown on the actionbar
# min_multiplier_only = true caps this item at the minimum multiplier only
items:
  - path: "Farming.page1.items.1"
    display: "Wheat"
  - path: "Farming.page1.items.2"
    display: "Carrot"
  - path: "Ores.page1.items.1"
    display: "Coal"
  - path: "Ores.page1.items.2"
    display: "Iron Ingot"
  - path: "Ores.page1.items.3"
    display: "Gold Ingot"
  - path: "Ores.page1.items.4"
    display: "Diamond"
    min_multiplier_only: true
  - path: "Mobs.page1.items.1"
    display: "Bone"
  - path: "Mobs.page1.items.2"
    display: "String"

# Notification types — enable or disable each independently
notifications:
  actionbar: true   # persistent bar above hotbar showing boosted items live
  chat: true        # chat message broadcast on boost start and end
  title: true       # title screen on boost start and end

# Actionbar display
display:
  actionbar_format: "&6BOOST: &e{items}"
  actionbar_separator: " &7| &e"

# Messages
messages:
  start_chat: "&6[SellBoost] &eSell boost started! &f{items}"
  end_chat: "&c[SellBoost] &7Boost ended. Normal prices resumed."
  start_title: "&6&lSELL BOOST!"
  start_subtitle: "&e{items}"
  end_title: "&c&lBOOST ENDED"
  end_subtitle: "&7Normal prices have resumed."
  title_fade_in: 10
  title_stay: 80
  title_fade_out: 20
```

---

## 🔍 Finding Your Item Paths

Open your EconomyShopGUI shop config files located in `plugins/EconomyShopGUI/shops/`. The path format is:

```
ShopFileName.page1.items.SLOT
```

**Example:** If your shop file is `Ores.yml` and Diamond is in slot 12:

```yaml
- path: "Ores.page1.items.12"
  display: "Diamond"
```

> If a path is invalid or the item is not sellable, SellBoost will log a warning on startup and skip it.

---

## 💻 Commands

Permission node: `sellboost.admin` — OP only by default

| Command | Description |
|---|---|
| `/sellboost start` | Trigger a boost manually right now |
| `/sellboost stop` | Stop the current active boost |
| `/sellboost status` | Show active items + time remaining, or countdown to next boost |
| `/sellboost reload` | Reload config without restarting |

---

## 🎮 How It Works

When a boost fires, SellBoost randomly picks items from your configured `items` list and assigns each one a random multiplier between `min` and `max`. All online players see the active boosted items on their actionbar in real time:

```
BOOST: Wheat (3x) | Coal (2.5x) | String (4x)
```

Only those specific items get the multiplier when sold through EconomyShopGUI. Everything else sells at normal price. Players who join mid-boost immediately see the actionbar.

When the server restarts mid-boost, the remaining time and active items are restored automatically from `data.yml`.

---

## 🔧 Requirements

- Paper / Spigot 1.21.x
- Java 21+
- EconomyShopGUI (free or premium)

---

## 🙏 Credits

Developed by **Treamhiler**
Support: discord.gg/tFXhkPVpxG
