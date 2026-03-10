# 🚀 SellBoost
A Paper plugin that integrates with **EconomyShopGUI** to run automatic randomized sell price boost events. At a configurable interval, the plugin picks random items from your shop and applies individual multipliers to their sell price — keeping your economy fresh and giving players a reason to stay active.

> 🔗 **More projects by Treamhiler:** [modrinth.com/user/Treamhiler](https://modrinth.com/user/Treamhiler)
> 💬 **Support & Downloads:** [discord.gg/tFXhkPVpxG](https://discord.gg/tFXhkPVpxG)
> 🐙 **GitHub:** [github.com/Treamhilerjava](https://github.com/Treamhilerjava)

---

## 📦 Installation
1. Drop `SellBoost.jar` into your server's `plugins/` folder
2. Ensure **EconomyShopGUI** (free or premium) is already installed
3. Restart the server
4. Edit `plugins/SellBoost/config.yml` with your actual shop item paths
5. Run `/sellboost reload`

---

## ✨ Features
- Automatic boost rotation at a configurable interval
- MULTIPLE or SINGLE boost mode — boost several items at once or just one
- Per-item multipliers with a random min/max/step range
- **Rolling multiplier** — the multiplier window gradually escalates over time, rewarding players who sell during later cycles
- **Live shop tooltip updates** — boosted sell prices are written directly to your shop files so players see the new price before they sell; originals are restored automatically when the boost ends
- **Server-wide boss bar** — shows boosted items, multipliers, and a live countdown during a boost; shows time until the next boost while idle
- Live actionbar showing boosted items and their multipliers
- Chat and title screen announcements — each independently toggleable
- Boost state persists across server restarts via `data.yml`
- Manual controls with `/sellboost start|stop|status|reload`

---

## 🎮 How It Works
When a boost fires, SellBoost picks random items from your configured list and assigns each a random multiplier. Players see it live on the boss bar and actionbar:

```
⚡ SELL BOOST | Wheat (3x) | Coal (2.5x) | String (4x) | 13m 34s
```

The sell price shown in `/shop` updates instantly to reflect the boost — no guessing required. When the boost ends, all prices are restored automatically. Only those specific items get the multiplier when sold through EconomyShopGUI. Everything else sells at normal price. Players who join mid-boost see it immediately.

---

## 💻 Commands
Permission node: `sellboost.admin` — OP only by default

| Command | Description |
|---|---|
| `/sellboost start` | Trigger a boost manually |
| `/sellboost stop` | Stop the current active boost |
| `/sellboost status` | Show active items, multiplier range, and time remaining |
| `/sellboost reload` | Reload config without restarting |

---

## ⚙️ Configuration
File: `plugins/SellBoost/config.yml`

```yaml
mode:
  type: MULTIPLE        # MULTIPLE | SINGLE
  multiple:
    count: 3            # how many items boosted at once
    no_repeat_last: true

rotation:
  unit: MINUTES         # HOURS | MINUTES | SECONDS
  value: 60

boost:
  duration:
    unit: MINUTES
    value: 15

multiplier:
  min: 2.0
  max: 4.0
  step: 0.5             # possible values: 2.0, 2.5, 3.0, 3.5, 4.0
  rolling:
    enabled: true
    interval:
      unit: HOURS
      value: 2
    ceiling: 6.0        # multiplier window stops escalating here, then wraps back

autosave:
  enabled: true
  interval_ticks: 200

notifications:
  actionbar: true       # live bar above hotbar
  chat: true            # chat message on start/end
  title: true           # title screen on start/end
  bossbar: true         # server-wide boss bar

display:
  bossbar:
    active_format: "&6⚡ SELL BOOST &8| &e{items} &8| &a{remaining}"
    idle_format: "&7Next boost in &e{time}"
    show_idle: true     # show boss bar between boosts

items:
  - path: "Farming.page1.items.1"
    display: "Wheat"
  - path: "Ores.page1.items.4"
    display: "Diamond"
    min_multiplier_only: true   # always gets minimum multiplier only
```

---

## 🔍 Finding Item Paths
Open your EconomyShopGUI shop config files in `plugins/EconomyShopGUI/shops/`. The path format is:

```
ShopFileName.page1.items.SLOT
```

Example — shop file `Ores.yml`, Diamond in slot 12:
```yaml
- path: "Ores.page1.items.12"
  display: "Diamond"
```

> If a path is invalid or the item is not sellable, SellBoost logs a warning and skips it.

---

## 🔧 Requirements
- Paper / Spigot 1.21.x
- Java 21+
- EconomyShopGUI (free or premium)

---

## 🙏 Credits
Developed by **Treamhiler**
[modrinth.com/user/Treamhiler](https://modrinth.com/user/Treamhiler) • [discord.gg/tFXhkPVpxG](https://discord.gg/tFXhkPVpxG) • [github.com/Treamhilerjava](https://github.com/Treamhilerjava)
