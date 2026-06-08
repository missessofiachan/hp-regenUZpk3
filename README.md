# Doom Health Regeneration Mod

A lightweight ZDoom mod that adds customizable health regeneration to your game. Perfect for adjusting the difficulty of your favorite WADs or adding modern shooter mechanics to classic Doom.

## Features

* **Fully Customizable:** Tweak regeneration settings directly from the in-game options menu.


* **Dynamic Settings:**
* **Regen Cap:** Set the maximum percentage of your Max HP that will regenerate.


* **Regen Amount:** Define how much health is restored per second.


* **Regen Delay:** Configure how many seconds of safety are required after taking damage before regeneration kicks in.




* **Difficulty Presets:** Quickly switch between pre-configured playstyles, ranging from "Power Trip" to "Hardcore," or try out styles inspired by games like *Wolfenstein* and *Call of Duty*.



## Configuration

You can modify the following server variables (CVars) via the console or the **Health Regen Settings** submenu found in your **Options** menu:

| CVar | Default | Description |
| --- | --- | --- |
| `mod_regen_cap` | 25 | Maximum health percentage for regeneration

 |
| `mod_regen_amount` | 5 | Health points recovered per second

 |
| `mod_regen_delay` | 5 | Seconds to wait after damage before healing begins

 |

## Technical Details

This mod is built for ZDoom-based source ports using ZScript. It utilizes:

* `EventHandler` for efficient `WorldTick` processing (checking every 35 tics) and monitoring damage events.


* `OptionMenu` definitions for a seamless UI integration within the game.



## Installation

1. Ensure you are running a ZDoom-compatible source port (e.g., UZDoom).
2. Drop the `.pk3` file into your mods folder or load it via your launcher.
3. Access the settings via **Options > Health Regen Settings** while in-game.



---

Developed for ZDoom compatibility.
