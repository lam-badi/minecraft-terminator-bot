# Terminator Boss Hunter for Minecraft – Technical Specification and Mod Concept

> **Document Version:** 1.1  
> **Target Platform:** Java mod for Minecraft (Forge / Fabric)  
> **Supported Game Versions:** 1.12 – latest

---

## Imagine...

Playing Minecraft with friends where you have **20 minutes of peace** to build a base and gather resources. After that, a **relentless, unkillable hunter** (codename: **"Terminator"**) spawns and begins an interdimensional manhunt.

He breaks through walls (soft blocks – instantly, obsidian – several times faster than a player), builds bridges over water, pours water buckets on lava, pursues you through portals to the Nether and End, and if you try to hide in different dimensions – he teleports after you. Killed him? In 20 minutes he respawns with +10% health. And so on, indefinitely.

Can you survive? This mod adds a co-op survival experience against a powerful AI opponent to Minecraft. Below is the complete technical specification for development.

---

## 1. General Concept

The mod adds a special boss-hunter with artificial intelligence to Minecraft. The core mechanic is a confrontation between a group of players and an unrelenting pursuer who gives a head start for base building, then begins a ruthless hunt. The players' goal is to survive as long as possible using tactics, environment, and cooperation.

## 2. Game Logic and Phases

### Phase 1: Preparation (Timer)
- When the mod is activated (via command or configuration), a countdown starts – **20 minutes** (value configurable).
- The Terminator is inactive: either stands still or is absent from the world. Players get time to build shelter, gather resources, and prepare for defense.
- Atmospheric effects (distant rumble, ground trembling) may hint at the approaching threat.

### Phase 2: The Hunt
- When the timer expires, the Terminator activates and begins pursuing players.
- Movement speed is always maximum (speed effect or increased base walk/run speed).

## 3. Terminator Characteristics and Mechanics

### Block Destruction
- The Terminator doesn't use tools but breaks blocks with his bare hands with special efficiency:
  - **Soft blocks** (dirt, wood, stone, cobblestone) – instantly or significantly faster than a player.
  - **Hard blocks** (diamond block, iron, obsidian) – slower than soft blocks, but still several times faster than a player with a diamond pickaxe.

### Basic Minecraft Knowledge
- The AI can overcome obstacles: jump, pillar up to climb vertical walls.
- Understands that players might burrow: if the target is underground, the Terminator digs straight down to close the distance.
- Uses the shortest path through obstacles (digging, building).

### Combat Characteristics
- **Health (HP):** base health – 320 HP (4 times a player's health, 80 HP * 4). Each respawn increases HP by 10% of the previous value.
- **Damage:** three hits kill an unarmored player (approximately 33 damage per hit).

## 4. Victory Conditions and Balance

- Players must survive as long as possible. Defeating the Terminator is only possible with good equipment (at least diamond sword/bow and full diamond armor).
- If players kill the Terminator, he respawns after 20 minutes (timer resets), gaining +10% maximum health. The cycle repeats indefinitely.

## 5. Technical Spawn and Pursuit Conditions

### Spawn Zone
- Initial spawn – when the mod is activated via command.
- Subsequent spawns – after death, within a radius of no more than **500 chunks** from the activation point (configurable, default 100).
- The spawn point is always within the specified radius of the player who initiated the launch.

### Pursuit and Visibility
- The Terminator "sees" players through any blocks (through walls and underground). He always knows their coordinates.
- The route is built along the shortest path considering obstacles (digging, building).
- If players flee and the distance exceeds the limit (configurable, default 500 chunks), the Terminator activates **speed boost mode**: his speed increases to creative (maximum) until he approaches any player within 100 chunks. Then speed returns to base.

## 6. Additional Mechanics (Immersion and Adaptation)

1. **Presence Traces** – during the preparation phase, sound/visual effects may occur (rumble, trembling).
2. **Adaptation to Player Actions** (simplified version):
   - If players frequently use bows, the Terminator may place temporary blocks (shields) in front of himself.
   - If players run across water – he walks along the bottom or builds a bridge.
   - If players hide in wooden structures – he may use flint and steel (item is automatically provided when needed).
3. **Detection System** – periodic "pulse" that highlights players within a 100-block radius (even through walls) for a few seconds.

## 7. Priorities and Environment Interaction

- The primary goal is eliminating players. Hostile mobs are only attacked if they block the path or hinder pursuit (e.g., a zombie cluster in a narrow tunnel).

## 8. Water Navigation and Crafting (Simplified Implementation)

- The Terminator **does not swim** – always walks along the bottom, receiving minimal water resistance (effect similar to sneaking or soul speed).
- If players escape by boat, the Terminator receives a **ready-made boat** (automatically provided) and uses it for pursuit. Similarly with flint and steel, water buckets, and other items – they appear in inventory as needed, in limited quantities (configurable).
- This can be replaced with full crafting in the future (the architecture allows for expansion).

## 9. Learning and Adaptation Within a Session

- The Terminator remembers certain player actions during one session (until the mod restarts). For example, if players often build wooden shelters – priority for using flint and steel increases. Data resets on restart.
- TNT avoidance: after several explosions, the Terminator learns to avoid traps (or pick up and move TNT, if possible in the simplified model).

## 10. Bot Settings (Configuration Menu)

All parameters are available through a configuration file (or GUI screen):

- Difficulty level (affects aggressiveness, accuracy, and tactics).
- Base health and HP multiplier for each respawn.
- Movement speed (base and boosted).
- Block destruction speed (separate for soft/hard blocks).
- Ability to set the Terminator's skin (texture).
- Respawn time (preparation timer).
- Spawn radius from player (in chunks).
- Number of simultaneously active Terminators (1–3, default 1).
- Maximum pursuit distance (default 500 chunks).
- Speed boost threshold and return-to-base-speed radius.
- Limits on automatically provided items (boats, buckets, etc.).

## 11. Creative Mode

- If at least one player switches to Creative mode, the Terminator stops all actions and becomes invulnerable.
- When the player exits Creative mode, the Terminator resumes the hunt from the same state (without restarting the timer).

## 12. Block Collection and Inventory Management

- While breaking blocks, the Terminator only picks up resources that are blocks (stone, dirt, wood, cobblestone, etc.). Small items (seeds, sticks, flowers) are ignored.
- Collected blocks are used for:
  - Quick pillar building.
  - Filling lava or water.
  - Constructing temporary shelters.
- Upon death, the Terminator may drop a percentage of collected resources (configurable).

## 13. Lava Attitude and Water Usage

- Lava deals **40 HP per second** to the Terminator. He perceives it as a critical threat and immediately seeks a detour or fills the lava with blocks from his inventory.
- If the path is blocked by a lava moat, the Terminator **receives a ready-made water bucket** (or several, according to settings) and pours water on the lava, opening a passage.

## 14. General Knowledge of Minecraft Mechanics (Simplified)

The mod lays the foundation for the following capabilities (many will be implemented later or replaced by item provision):

- Use of key items (boats, buckets, flint and steel).
- Understanding of liquid physics.
- Advanced movement (jumping, elytra – optional).
- Siege tactics (setting fires, filling moats).

The mod's architecture allows for easy future expansion (adding full crafting, more sophisticated AI).

## 15. Interdimensional Pursuit

- The Terminator can follow players through portals to the Nether and End.
- If a portal works normally, the Terminator enters it after the player (lights it with flint and steel if necessary).
- If the portal is temporarily unavailable (broken, deactivated, used in creative mode), a timer starts (default **2 minutes**). When the timer expires, the Terminator teleports to the target's dimension, appearing within **50 chunks** of them (value configurable). Teleportation is only used when the portal cannot be used.
- **Returning from the End:** since the return portal only appears after killing the dragon, the Terminator teleports back to the Overworld to the nearest player (or to the spawn point if no players are present). Entry to the End is always through a portal.

### Target Prioritization When Players Are Split Across Dimensions

- **Rule 1:** If players are in different dimensions, the Terminator first goes to the dimension with more players.
- **Rule 2:** If equal (e.g., one in each dimension), priority is given to the dimension where a player recently respawned. If no such information exists – the closest dimension by absolute coordinates is chosen (simplified).
- **Rule 3 (anti-cheat):** If players deliberately split up with one in each of the three dimensions, the Terminator activates direct teleportation mode: sequentially eliminates players, ignoring portals. Teleportation works on a timer (e.g., every 2 minutes) until all targets are in the same dimension.

### Portal Destruction After Return

- After the Terminator passes through a portal following players and eliminates them in another dimension, upon returning to the original world he destroys the portal (minimum 5 blocks of obsidian or frame material) to prevent repeated escape. If the portal was built by the Terminator himself, he does not destroy it.

## 16. Physical Properties and Flawless Behavior

- The Terminator **takes no fall damage** from any height.
- The AI strives for flawless use of mechanics, but within realistic complexity. Minor errors are acceptable (e.g., accidentally falling into lava followed by quick exit). However, he never commits deliberately suicidal actions.

## 17. Compatibility and Version Requirements

- The mod supports Minecraft starting from version **1.12** up to the latest at the time of development.
- Implementation uses current knowledge bases of game mechanics, but additional materials (tags, crafting descriptions) can be provided if needed.

## 18. Implementation Clarifications (Answers to Potential Questions)

### Platform and Language
- The mod is written in **Java** using **Minecraft Forge** or **Fabric**. This is the standard way to create mods, requiring no external APIs.
- For compatibility with single-player and servers, the mod is installed as a regular `.jar` file in the `mods` folder.

### AI Simplification (Items on Demand)
- To avoid excessive complexity, complex crafting chains are replaced with **automatic item provision** (boat, water bucket, flint and steel) when the AI decides to use them. The number of provisions is limited by settings (can be made infinite).
- The code includes architecture allowing future replacement of provision with full crafting (via the `IRecipe` interface).

### Chunk Loading and Performance
- Default maximum pursuit distance is **100 chunks** (configurable up to 500). This reduces server load. Distant chunks are not constantly loaded – a lazy loading mechanism is used as movement progresses.
- If the Terminator falls behind by more than the `limit` chunks, he enters speed boost mode and catches up to the player, forcibly loading necessary chunks.

### Coordinates and Portals
- When teleporting between dimensions, simple math is used: the Terminator appears within **50 chunks** of the target (configurable). Coordinates are recalculated considering the Nether scale (factor 8).
- If a portal is available, the AI will prefer to enter it rather than teleport.

### Multiplayer Scenarios
- **Nearest player** – determined by Euclidean distance in the current dimension. If players are in different dimensions, priority goes to the dimension with the most players.
- In edge cases (1/1/1), the anti-cheat mode activates (teleportation).

### Limits and Exceptions
- Falling behind by more than `limit` chunks (default 500) activates speed boost to creative speed. Boost lasts until distance to any player becomes less than 100 chunks.
- If the Terminator gets stuck in geometry (e.g., due to generation bugs), he tries to escape by digging in a random direction or teleports to the nearest surface.

### Creative Mode
- When a player switches to creative, the Terminator freezes and becomes invulnerable. When all players exit creative mode, he resumes the hunt from the same location.

### Inventory and Drops
- The Terminator's inventory is limited (e.g., 27 slots). He stores only blocks and items needed for current tasks.
- Upon death, the Terminator drops a configurable percentage of collected resources (default 50%). This adds purpose to hunting him.

## 19. Required Technologies, Libraries, and Integrations

- **Java JDK 8** or newer.
- **Development Environment:** IntelliJ IDEA / Eclipse.
- **Minecraft Forge MDK** (recommended) or Fabric.
- **Git** for version control.
- **Gradle** (included in MDK) for building.
- For navigation, Minecraft's built-in classes are used (`PathNavigate`, etc.).
- Logging – SLF4J (already in Forge).
- Configuration – via JSON or TOML (can use Forge's library).

## 20. Expected Deliverables

1. Complete mod code with comments in Russian (or English).
2. Step-by-step installation instructions (where to place `.jar`, how to configure).
3. List of dependencies (only Forge/Fabric and standard libraries).
4. Example configuration file with all parameters.

---

**The document is ready for discussion and implementation. All key points are agreed upon, and the architecture allows for future functionality expansion.**
