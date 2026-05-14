````markdown
<div align="center">

# ⚔️ mod-startergear

### A modern starter gear module for AzerothCore WotLK 3.3.5a

<p align="center">
  <a href="https://github.com/azerothcore/azerothcore-wotlk">
    <img src="https://img.shields.io/badge/AzerothCore-Module-0ea5e9?style=for-the-badge&logo=github&logoColor=white">
  </a>
  <a href="https://www.azerothcore.org/">
    <img src="https://img.shields.io/badge/WoW-3.3.5a-facc15?style=for-the-badge">
  </a>
  <img src="https://img.shields.io/badge/C%2B%2B-17-f97316?style=for-the-badge&logo=cplusplus&logoColor=white">
  <img src="https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Status-Production_Ready-10b981?style=flat-square">
  <img src="https://img.shields.io/badge/Auto_SQL-Supported-8b5cf6?style=flat-square">
  <img src="https://img.shields.io/badge/Configurable-Yes-06b6d4?style=flat-square">
  <img src="https://img.shields.io/badge/WotLK-Heirlooms-ec4899?style=flat-square">
</p>

---

### ✨ Give freshly created characters a real head start.

Class-specific heirlooms, bags, riding skills, mounts and bonus XP rewards — all delivered instantly with a single command.

---

</div>

<br>

# 📚 Table of Contents

- [✨ Features](#-features)
- [🧠 How It Works](#-how-it-works)
- [📦 Installation](#-installation)
- [⚙️ Configuration](#️-configuration)
- [📋 Item Reference](#-item-reference)
- [🧙 Class Gear Overview](#-class-gear-overview)
- [🗄️ Database Schema](#️-database-schema)
- [🛠️ For Developers](#️-for-developers)
- [❓ FAQ](#-faq)
- [📄 License](#-license)

---

# ✨ Features

<div align="center">

| Feature | Description |
|:--|:--|
| 🎒 **Starter Bags** | Configurable bag item and amount for all characters |
| ⚔️ **Class Heirlooms** | Automatic class-specific heirloom sets |
| 💍 **XP Ring Included** | Grants the legendary **Dread Pirate Ring** |
| 🐴 **Riding at Level 1** | Gives riding skills instantly via `learnSpell()` |
| 🗡️ **Multi-Spec Support** | Hybrid classes receive multiple gear paths |
| 🔒 **One-Time Usage** | Protected by character database tracking |
| 😂 **Funny Responses** | Random witty messages for repeat attempts |
| ⚙️ **Fully Configurable** | Enable/disable every major feature |
| 🗄️ **Automatic SQL** | SQL updates handled by AzerothCore automatically |

</div>

---

# 🧠 How It Works

When a player types:

```bash
.startergear
```

the module executes the following flow:

```text
Player Command
      │
      ▼
Config Validation
      │
      ▼
Class Validation
      │
      ▼
Database Usage Check
      │
      ├── Already used?
      │        └── Funny denial message
      │
      ▼
Grant Starter Rewards
      │
      ├── Bags
      ├── Riding Skills
      ├── Mount
      ├── XP Ring
      └── Heirloom Gear
      │
      ▼
Store Character GUID
```

---

## 🐴 Riding at Level 1

The module uses:

```cpp
Player::learnSpell()
```

which directly injects riding spells into the player's spellbook without validating level requirements.

That means:

- ✅ No core edits required
- ✅ No hacks needed
- ✅ Fully AzerothCore compatible

The included SQL patch additionally changes the mount item's:

```sql
RequiredLevel = 1
```

so the tooltip also correctly displays:

> Requires Level 1

---

# 📦 Installation

## Requirements

| Requirement | Version |
|:--|:--|
| AzerothCore | Recent master branch |
| Compiler | C++17 compatible |
| Supported OS | Linux / Windows |

---

## 1️⃣ Clone the Module

```bash
cd /path/to/azerothcore/modules

git clone https://github.com/hypopheria2k/mod-startergear.git
```

---

## 2️⃣ Re-run CMake

```bash
cmake -B build .
```

---

## 3️⃣ Compile

### Linux

```bash
cd build
make -j$(nproc)
```

### Windows (Visual Studio)

```powershell
cmake --build . --config Release
```

---

## 4️⃣ Install Config

```bash
cp modules/mod-startergear/conf/mod-startergear.conf.dist \
configs/modules/mod-startergear.conf
```

---

## 5️⃣ Start the Worldserver

```bash
./worldserver
```

AzerothCore will automatically detect and apply the included SQL updates.

---

# ⚙️ Configuration

Configuration file location:

```text
configs/modules/mod-startergear.conf
```

---

## Example Configuration

```ini
#
# StarterGear Configuration
#

# Enable / Disable Module
StarterGear.Enable = 1

# Starter Bags
StarterGear.BagId = 41600
StarterGear.BagCount = 4

# Riding + Mount
StarterGear.GiveRiding = 1
StarterGear.MountId = 54811

# Class Toggles
StarterGear.Class.1.Enable = 1    # Warrior
StarterGear.Class.2.Enable = 1    # Paladin
StarterGear.Class.3.Enable = 1    # Hunter
StarterGear.Class.4.Enable = 1    # Rogue
StarterGear.Class.5.Enable = 1    # Priest
StarterGear.Class.6.Enable = 1    # Death Knight
StarterGear.Class.7.Enable = 1    # Shaman
StarterGear.Class.8.Enable = 1    # Mage
StarterGear.Class.9.Enable = 1    # Warlock
StarterGear.Class.11.Enable = 1   # Druid
```

---

# 📋 Item Reference

## 🛡️ Chest & Shoulder Heirlooms

| Item ID | Name | Armor Type | Main Stat |
|:--|:--|:--|:--|
| `48691` | Tattered Dreadmist Robe | Cloth | Intellect |
| `48689` | Stained Shadowcraft Tunic | Leather | Agility |
| `48687` | Preened Ironfeather Breastplate | Leather | Intellect |
| `48677` | Champion's Deathdealer Breastplate | Mail | Agility |
| `48683` | Mystical Vest of Elements | Mail | Intellect |
| `48685` | Polished Breastplate of Valor | Plate | Strength |

---

## ⚔️ Weapon Heirlooms

| Item ID | Name | Type | Stat |
|:--|:--|:--|:--|
| `42947` | Dignified Headmaster's Charge | Staff | Spell Power |
| `42943` | Bloodied Arcanite Reaper | 2H Axe | Strength |
| `42948` | Devout Aurastone Hammer | 1H Mace | Spell Power |
| `48716` | Venerable Mass of McGowan | 1H Mace | Agility |
| `42945` | Venerable Dal'Rend's Sacred Charge | 1H Sword | Attack Power |
| `42944` | Balanced Heartseeker | Dagger | Agility |
| `42946` | Charmed Ancient Bone Bow | Bow | Ranged |

---

## 💍 Trinkets & Special Items

| Item ID | Name | Effect |
|:--|:--|:--|
| `50255` | Dread Pirate Ring | +5% Experience |
| `42991` | Swift Hand of Justice | Haste / Heal on Kill |
| `42992` | Discerning Eye of the Beast | Spell Power / Mana Restore |

---

# 🧙 Class Gear Overview

| Class | Armor | Weapons | Extras |
|:--|:--|:--|:--|
| Mage / Warlock / Priest | Cloth Int | Staff | 2× Caster Trinkets + Ring |
| Druid | Leather Int + Agi | Staff | Melee + Caster Support |
| Rogue | Leather Agi | Daggers + Bow | Dual Melee Trinkets |
| Hunter | Mail Agi | Bow + 1H | Ranged Setup |
| Shaman | Mail Int + Agi | 1H Weapons | Hybrid Support |
| Warrior / DK / Paladin | Plate Str | 2H Axe + 1H | Melee + Hybrid |

---

# 🗄️ Database Schema

## Character Database

### `custom_startergear_used`

```sql
CREATE TABLE IF NOT EXISTS `custom_startergear_used` (
    `guid` INT UNSIGNED NOT NULL,
    `used_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (`guid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

---

# 🛠️ For Developers

## Module Structure

```text
mod-startergear/
│
├── conf/
├── data/
│   ├── sql/
│   │   ├── characters/
│   │   └── world/
│
├── src/
│   ├── StarterGear.cpp
│   ├── StarterGear.h
│   └── mod_startergear_loader.cpp
│
├── CMakeLists.txt
└── README.md
```

---

## Design Goals

- Clean and lightweight
- Zero core modifications
- Fully configurable
- Retail-like starter experience
- Easy maintenance
- AzerothCore standards compliant

---

# ❓ FAQ

<details>
<summary><strong>Can players use the command more than once?</strong></summary>

No. Every character GUID is permanently stored in the character database after the first use.

</details>

<details>
<summary><strong>Why do hybrid classes receive extra gear?</strong></summary>

To support all specs immediately — for example healing, tanking and DPS.

</details>

<details>
<summary><strong>Does this require core edits?</strong></summary>

No. The module works entirely through the AzerothCore module API.

</details>

<details>
<summary><strong>Does this work with existing characters?</strong></summary>

Yes. Any character that has not already used `.startergear` can use it once.

</details>

---

# 📄 License

This project is licensed under the **MIT License**.

---

<div align="center">

## ❤️ Built for the AzerothCore Community

### *"Because every hero deserves a proper start."*

<br>

<img src="https://img.shields.io/badge/Made%20with-Love-e11d48?style=for-the-badge">
<img src="https://img.shields.io/badge/WotLK-3.3.5a-facc15?style=for-the-badge">
<img src="https://img.shields.io/badge/AzerothCore-Compatible-0ea5e9?style=for-the-badge">

</div>
````
