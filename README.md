<div align="center">

# 🚀 SellBoost

**Randomized sell price boost events for EconomyShopGUI**

[![Modrinth](https://img.shields.io/modrinth/v/sellboost?label=Modrinth&logo=modrinth&color=1bd96a)](https://modrinth.com/plugin/sellboost)
[![Discord](https://img.shields.io/discord/1234567890?label=Discord&logo=discord&color=5865F2)](https://discord.gg/tFXhkPVpxG)
[![Java](https://img.shields.io/badge/Java-21-orange?logo=openjdk)](https://adoptium.net/)
[![Paper](https://img.shields.io/badge/Paper-1.21.x-white?logo=spigotmc)](https://papermc.io/)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

</div>

---

At a configurable interval, SellBoost picks random items from your EconomyShopGUI shop and applies individual multipliers to their sell price — keeping your economy dynamic and giving players a reason to stay active. Shop tooltips update in real time, and a server-wide boss bar keeps everyone informed.

---

## ✨ Features

- **MULTIPLE / SINGLE** boost mode — boost several items at once or just one
- **Per-item multipliers** — random values within a configurable min/max/step range
- **Rolling multiplier** — the range escalates each cycle up to a ceiling, then wraps back
- **Live shop tooltip updates** — boosted prices written to shop YAMLs on start, restored on end
- **Server-wide boss bar** — shows items, multipliers, and countdown; idle state shows next boost timer
- **Actionbar display** — live feed above the hotbar during a boost
- **Chat + title announcements** — each independently toggleable
- **`no_repeat_last`** — prevents the same items appearing in back-to-back boosts
- **`min_multiplier_only`** per item — always uses the base minimum (useful for rare items)
- **Persistent state** — active items, timers, and rolling epoch survive server restarts via `data.yml`

---

## 📋 Requirements

| Requirement | Version |
|---|---|
| Paper / Spigot | 1.21.x |
| Java | 21+ |
| EconomyShopGUI | Free or Premium |

---

## 🚀 Installation

1. Drop `SellBoost.jar` into your `plugins/` folder
2. Ensure **EconomyShopGUI** is installed
3. Restart the server
4. Edit `plugins/SellBoost/config.yml` — add your item paths and tune your multipliers
5. Run `/sellboost reload`

---

## ⚙️ Configuration

```yaml
mode:
  type: MULTIPLE        # MULTIPLE | SINGLE
  multiple:
    count: 3
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
  step: 0.5
  rolling:
    enabled: true
    interval:
      unit: HOURS
      value: 2
    ceiling: 6.0        # range stops escalating here, then wraps back to base

autosave:
  enabled: true
  interval_ticks: 200

notifications:
  actionbar: true
  chat: true
  title: true
  bossbar: true

display:
  bossbar:
    active_format: "&6⚡ SELL BOOST &8| &e{items} &8| &a{remaining}"
    idle_format:   "&7Next boost in &e{next}"
    show_idle:     true

items:
  - path: "Farming.page1.items.28"
    display: "Wheat"
  - path: "Ores.page1.items.16"
    display: "Iron Ingot"
  - path: "Ores.page1.items.9"
    display: "Diamond"
    min_multiplier_only: true
```

### Finding Item Paths

Open your shop files in `plugins/EconomyShopGUI/shops/`. The path format is:

```
ShopFileName.page1.items.SLOT
```

> If a path is invalid or the item is not sellable, SellBoost logs a warning and skips it on boot.

---

## 💻 Commands & Permissions

| Command | Permission | Description |
|---|---|---|
| `/sellboost start` | `sellboost.admin` | Trigger a boost manually |
| `/sellboost stop` | `sellboost.admin` | Stop the current boost |
| `/sellboost status` | `sellboost.admin` | Show items, multiplier range, rolling epoch, countdown |
| `/sellboost reload` | `sellboost.admin` | Reload config without restarting |

> `sellboost.admin` defaults to OP.

---

## 📁 Project Structure

```
src/main/java/org/sellboost/
├── SellBoost.java           # Plugin entry point
├── BoostManager.java        # Boost lifecycle, scheduling, and state
├── RollingMultiplier.java   # Escalating multiplier window logic
├── BossBarManager.java      # Server-wide boss bar
├── ShopFileEditor.java      # YAML price editing and restore
├── ShopHook.java            # EconomyShopGUI item resolution
├── ShopListener.java        # PreTransactionEvent price multiplier
├── BoostedItem.java         # Boost item model
├── BoostCommand.java        # /sellboost command
├── ConfigManager.java       # Config key access
├── DataManager.java         # data.yml persistence
└── JoinListener.java        # Boss bar player add/remove
```

---

## 📜 Changelog

See [CHANGELOG.md](CHANGELOG.md)

---

<div align="center">

💬 **[Discord](https://discord.gg/tFXhkPVpxG)** · 🔗 **[Modrinth](https://modrinth.com/user/Treamhiler)** · 🐙 **[GitHub](https://github.com/Treamhilerjava)**

Made by **Treamhiler**

</div>
