# Health Regeneration Mod for ZDoom / GZDoom

A lightweight, highly customizable ZScript mod that adds dynamic health regeneration mechanics to Doom. Whether you want to recreate modern shooter pacing (like *Call of Duty*), tactical segment-based healing (like *Wolfenstein* or *Quake Champions*), or fine-tune your own custom challenge, this mod provides all the options you need.

---

## 🚀 Key Features

* **Two Unique Healing Modes:** Switch between Standard Cap (percentage-based) and a fully customizable Segment-Based (chunked) regeneration.
* **Custom Health Segments:** Define exactly how large your health chunks are to perfectly tailor the game's tactical pacing.
* **In-Game Settings Menu:** Fine-tune every aspect of regeneration directly from the **Options > Health Regen Settings** menu.
* **Pre-configured Presets:** Quickly apply themed presets (Wolfenstein, Quake, Call of Duty) or standard difficulty presets ranging from *Power Trip* (Easy) to *Hardcore* (Hard).
* **Movement Multipliers:** Bonus healing scaling when crouching or standing still.
* **Stand-Still Restriction Switch:** A toggle to restrict health regeneration strictly to when the player is stationary.
* **Audio-Visual Feedback:** Optional custom visual sparkles/particles and soft healing sound effects that trigger when health is actively restored.

---

## 🛠️ Configuration & CVars

You can adjust all variables in the console or via the **Health Regen Settings** menu.

| Console CVar | Default | Allowed Range | Description |
| --- | --- | --- | --- |
| `mod_regen_enabled` | `true` | `true` / `false` | Enable or disable the entire regeneration handler. |
| `mod_regen_mode` | `0` | `0`, `1` | **0:** Standard Cap %, **1:** Segment-Based |
| `mod_regen_cap` | `25` | `5` to `200` | Maximum health percentage you can regenerate to (Standard mode only). |
| `mod_regen_segment_size` | `20` | `5` to `100` | Size of the health chunks (Segment-Based mode only). |
| `mod_regen_amount` | `5` | `1` to `100` | Base health points (HP) restored per second. |
| `mod_regen_delay` | `5` | `0` to `30` | Safety window (seconds) after taking damage before regeneration begins. |
| `mod_regen_crouch_mult` | `1.0` | `1.0` to `5.0` | Speed multiplier applied when the player is crouching. |
| `mod_regen_still_mult` | `1.0` | `1.0` to `5.0` | Speed multiplier applied when the player is standing still. |
| `mod_regen_only_still` | `false` | `true` / `false` | If enabled, healing is suspended entirely while moving. |
| `mod_regen_particles` | `true` | `true` / `false` | Enable or disable visual fullbright particle effects when healing. |
| `mod_regen_sound` | `true` | `true` / `false` | Enable or disable the healing sound effect (`misc/i_pk_up`). |

---

## 🔄 Regeneration Modes Explained

### 1. Standard Cap % (`mod_regen_mode 0`)

Regeneration restores health up to a static percentage of your player's maximum HP (e.g., 25 HP for a standard 100 HP cap). If your health is above this threshold, no regeneration occurs.

### 2. Segment-Based Regeneration (`mod_regen_mode 1`)

Instead of restoring health to a static percentage cap, this mode divides your health pool into sequential, independent **segments** (or "health chunks") based on the `mod_regen_segment_size` CVar.

#### How Segment Regeneration Behaves:

* Health **only regenerates up to the boundary of your currently active segment**. It will never cross over into a higher segment automatically.
* To climb into a higher segment, you must pick up active health items (such as Stimpacks, Medkits, or Blue Potions) to cross the boundary line. Once crossed, regeneration will now heal you up to the ceiling of that new segment.
* **Example (Using a Custom 20 HP Segment Size):**
* If your health falls to **12 HP**, you are in the *0-20 HP* segment. You will regenerate up to **20 HP**.
* If you collect a Stimpack and push your health to **22 HP**, you enter the *21-40 HP* segment. You will now regenerate up to **40 HP**.
* If you take damage down to **45 HP**, you are in the *41-60 HP* segment. You will regenerate up to **60 HP**.



---

## 🏃 Stillness & Crouching Multipliers

Healing rate can be scaled dynamically depending on player state:

* **Multiplier Stacking:** If both `mod_regen_crouch_mult` and `mod_regen_still_mult` are set above `1.0`, they stack multiplicatively.
* **Horizontal vs. Vertical Movement:** Stillness is evaluated based only on **horizontal/lateral velocity** (X and Y axes). This ensures that jumping, falling, or riding vertical elevators does not break your "standing still" bonus or suspend healing when `mod_regen_only_still` is enabled.

---

## ⚡ Built-in Presets

Quick-select presets are available at the bottom of the Options Menu:

### Standard Difficulty Presets

* **Power Trip (Easy):** 100% Cap, 15 HP/sec, 2-second delay.
* **Casual (Medium-Easy):** 50% Cap, 10 HP/sec, 3-second delay.
* **Balanced (Normal):** 25% Cap, 5 HP/sec, 5-second delay.
* **Tough (Medium-Hard):** 20% Cap, 2 HP/sec, 5-second delay.
* **Hardcore (Hard):** 15% Cap, 1 HP/sec, 7-second delay.

### Game Themed Presets

* **Wolfenstein: The New Order:** 20 HP Segment Mode, 5 HP/sec, 5-second delay.
* **Quake Champions (B.J. Blazkowicz):** 25 HP Segment Mode, 5 HP/sec, 3-second delay.
* **Call of Duty:** 100% Cap (Full heal), 20 HP/sec, 5-second delay.

*Note: Selecting any preset will automatically reset "Only Heal When Still" (`mod_regen_only_still`) to `false`.*

---

## 💻 Technical Details

This mod is implemented in **ZScript** (requiring ZDoom 4.11+ source ports):

* **`EventHandler` Logic:** Checks player states once every 35 tics (1 second) in `WorldTick` to keep performance overhead virtually non-existent.
* **Dynamic Damage Delay:** Uses `WorldThingDamaged` to trigger the configured safety delay period accurately when a player takes damage.

---

## 💾 Installation

1. Download and compile the mod as a `.pk3` or `.zip` file (or load the folder directly in source ports that support directory loads).
2. Load the mod using your preferred GZDoom launcher (e.g., ZDL) or drag-and-drop the mod onto the source port executable.
3. Open the game, head to **Options > Health Regen Settings**, and customize your settings.