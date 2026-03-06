# Hex Conquest — Project Context

## Overview

Hex Conquest is a turn-based strategy game inspired by games like Civilization, Risk, and Paradox strategy systems.

The game is played on a procedurally generated hexagonal map.  
Players control territories, gather resources, build armies, perform intelligence operations, and wage war to dominate the map.

The project is built as a **client-server web application**.

- Backend: Python
- Frontend: HTML / CSS / JavaScript
- Map rendering: JavaScript hex grid

The goal of the game is to:

• eliminate all other players  
OR  
• control at least **70% of the map**  

If the game reaches **200 turns**, the winner is the player with the **largest and richest empire**.

---

# Core Game Concepts

## Hexagonal Map

The game map is composed of **hexagonal tiles**.

Each tile contains:

- a biome
- resources
- an owner (or neutral)
- possible units
- stability level

The map is **procedurally generated using seeds**, similar to Minecraft.

Players can input a **seed** to generate identical worlds.

Map sizes:

- Small
- Medium
- Large

Each map size defines a **maximum optimal number of players**.

---

# Biomes

Each hex tile has a biome which influences movement, resources and combat.

Available biomes:

- Water
- Plains
- Forest
- Mountain
- Desert
- Snow
- Ice
- River (modifier)

Biomes influence:

- movement cost
- resource generation
- defensive bonuses
- exploration difficulty

---

# Player Spawn

At the beginning of the game:

1. Players manually select a spawn hex
2. The spawn grants control of **7 hexes**
   - the center hex
   - the 6 surrounding hexes

This becomes the starting territory.

---

# Turn System

The game is **turn based**.

Turn order is **fixed**.

Each turn:

1. Player rolls **1d20**
2. The result becomes **Action Points**

Example:

Roll: 14  
Player receives **14 action points**

Actions consume a fixed number of action points.

Players may repeat actions multiple times if they have enough points.

---

# Action Categories

Each action belongs to a category requiring specific unit types.

Main action types:

### Intelligence

- Explore (reconnaissance)
- Spy
- Sabotage

### Military

- Attack
- Colonize neutral territory
- Move armies

### Economy

- Produce resources
- Extract resources
- Improve territory
- Trade

---

# Units and Armies

Units are grouped into **armies**.

Armies occupy hex tiles.

Different unit types exist (defined in `units/`):

Possible examples:

- infantry
- artillery
- reconnaissance units
- engineering units

Some actions require specific unit types.

Example:

- artillery allows **distance attacks**
- reconnaissance improves intelligence actions

---

# Combat System

Combat uses a mix of **strategy mechanics and dice rolls**.

Attack results depend on:

- unit strength
- terrain
- intelligence level
- sabotage effects
- dice rolls

Dice types may vary depending on combat situations.

Defined in:

combat/dice.py
combat/combat_system.py


---

# Special Combat Rules

### Artillery

Artillery can attack **adjacent hexes without entering them**.

This creates **unilateral combat**.

### River Attacks

Attacks may occur **across rivers** without entering the hex first.

---

# Resources

Each tile generates:

- common resources
- rare resources

Example resources:

Common:
- food
- wood
- stone

Rare:
- gold
- salt
- fish
- metals

Resource types depend on biome.

Example:

River:
- fish
- salt

Mountain:
- stone
- metal

Desert:
- rare minerals

---

# Economy System

Players can:

- produce resources
- extract resources
- improve territory
- trade resources

Defined in:


economy/resource_system.py
economy/production_system.py
economy/trade_system.py


---

# Territory Control

When conquering a territory, players choose an **occupation type**.

Defined in:


politics/occupation_types.py


Types:

### Annexed

- 100% production
- high revolt risk
- revolts disappear after pacification

### Colonized

- 85% production
- moderate revolt risk

### Occupied

- high production
- rare but stronger revolts

### Puppet State

- 75% production
- low revolt chance
- semi-autonomous
- may declare independence if instability rises

---

# Rebellion System

Defined in:


politics/rebellion_system.py


Rebellions cause:

- production instability
- movement disruption
- army desertion
- rebel armies spawning

Extreme rebellions can create:

- an **independent territory**

---

# Intelligence System

Players can perform covert operations:

- espionage
- sabotage
- reconnaissance

Defined in:


intelligence/espionage.py
intelligence/sabotage.py


Effects may include:

- revealing enemy units
- reducing production
- weakening armies

---

# Fog of War

The game uses **fog of war**.

Players can only see:

- their territory
- nearby explored regions
- areas revealed by reconnaissance

---

# Client-Server Architecture

## Backend

Python server handles:

- game state
- turns
- combat
- economy
- AI players

Main entry point:


server/app.py


Game logic:


game/
map/
units/
combat/
economy/
politics/


---

## Frontend

The frontend is a browser client.

Responsibilities:

- render the hex map
- display UI
- send player actions to server

Main files:


client/index.html
client/style.css
client/main.js


---

# Map Rendering

Hex map rendering is handled by:


client/map/hex_renderer.js
client/map/map_interaction.js


Features:

- hex grid rendering
- biome textures
- unit icons
- tile selection
- camera movement

Textures stored in:


assets/textures/biomes/
assets/textures/units/


---

# User Interface

UI components:


ui/hud.js
ui/action_panel.js
ui/turn_display.js


They display:

- player resources
- action buttons
- turn information

---

# Artificial Intelligence

AI players are implemented in:


game/ai_player.py


AI can:

- expand territory
- build armies
- attack enemies
- manage economy

---

# Project Goals

Hex Conquest is designed as a **large-scale strategy programming project**.

Objectives:

- modular architecture
- clear separation of systems
- expandable mechanics
- procedural world generation
- AI capable of playing autonomously

---

# Code Conventions

Python:

- object oriented
- modular systems
- separated responsibilities

Frontend:

- vanilla JavaScript
- modular files
- map renderer separated from UI

---

# Future Possible Features

Potential future additions:

- diplomacy system
- alliances
- technology research
- naval combat
- advanced AI behaviors
- multiplayer networking