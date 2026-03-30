# Pokémon Brilliant Diamond Egg Farming Bot

An automated egg farming bot for **Pokémon Brilliant Diamond** using **Ryujinx**, OCR, and virtual controller inputs.

---

## Features

* Automatic egg generation (movement loop)
* NPC interaction
* OCR-based dialogue detection
* Egg detection vs no-egg detection
* Automatic sending of eggs to PC
* Visual calibration using templates (NPC + player)

---

## Requirements

* Windows
* Python **3.10** or **3.11**
* Ryujinx emulator
* Pokémon Brilliant Diamond
* Virtual controller setup compatible with the `Controller` class

---

## Project Structure

```
pokemon-egg-bot/
│
├─ egg_bot.py
├─ requirements.txt
├─ utils/
│  └─ controller.py
└─ templates/
   ├─ npc.png
   ├─ player_1.png
   ├─ player_2.png
   ├─ player_3.png
   ├─ player_4.png
   ├─ player_5.png
   ├─ player_6.png
   ├─ player_7.png
   └─ player_8.png
```

---

## Installation

### 1. Install Python

Download and install Python 3.10 or 3.11.
Make sure to enable:

```
Add Python to PATH
```

Verify installation:

```bash
python --version
```

---

### 2. Create a virtual environment

```bash
python -m venv venv
venv\Scripts\activate
```

---

### 3. Install dependencies

Create a `requirements.txt` file:

```txt
opencv-python
mss
numpy
psutil
pywin32
rapidocr-onnxruntime
```

Install:

```bash
pip install -r requirements.txt
```

---

## Controller Setup

The script requires:

```python
from utils.controller import Controller
```

You must have:

```
utils/controller.py
```

This file must implement a `Controller` class with a method like:

```python
controller.macro("...")
```

---

## Template Images

The bot uses image recognition for calibration.

Required files:

* `npc.png` → the egg NPC
* `player_1.png` to `player_8.png` → player sprites

### Tips for templates

* Capture directly from Ryujinx
* Use the same resolution as gameplay
* Do not resize images
* Keep images clean and sharp
* Avoid motion blur

---

## Ryujinx Setup

Before running the bot:

1. Open Ryujinx
2. Launch Pokémon Brilliant Diamond
3. Go to the egg NPC location
4. Keep the window visible
5. Ensure controller configuration is correct

---

## Button Mapping

Default mapping:

```python
BTN_A = "B"
BTN_B = "A"
```

This swaps A/B for Ryujinx.

You can adjust if needed.

---

## Running the Bot

Activate your environment and run:

```bash
python egg_bot.py
```

---

## Calibration

At startup, the bot will ask you to position your character:

```
Place your character at the ideal starting position in front of the NPC.
Press Enter when ready...
```

This step is critical.

The bot will detect:

* NPC position
* Player position
* Offset between them

---

## How It Works

The bot loop:

1. Moves right
2. Performs egg generation steps
3. Returns to NPC
4. Interacts
5. Reads dialogue via OCR
6. Either:

   * Collects egg and sends to PC
   * Closes dialogue if no egg

---

## Stop the Bot

Press:

```
Ctrl + C
```

---

## Debug Options

### OCR Debug

Enable:

```python
DEBUG_SAVE_IMAGES = True
```

Output folder:

```
debug_ocr/
```

---

### Vision Debug

Output folder:

```
debug_vision/
```

Shows detected NPC and player positions.

---

## Common Issues

### Ryujinx window not found

* Ensure Ryujinx is open
* Do not minimize the window

---

### Templates not found

* Verify all files exist in `/templates`
* Check file names

---

### Calibration fails

* Improve template quality
* Ensure correct player position
* Keep same resolution
* Adjust thresholds:

```python
NPC_TEMPLATE_THRESHOLD = 0.42
PLAYER_TEMPLATE_THRESHOLD = 0.54
```

---

### OCR not working properly

* Avoid graphical filters
* Keep resolution consistent
* Enable debug images

---

### Wrong button inputs

Adjust:

```python
BTN_A
BTN_B
```

---

### Bot misses NPC

* Check starting position
* Improve templates
* Adjust movement values:

```python
INITIAL_RIGHT_TAPS
HORIZONTAL_REPEATS
RECENTER_MAX_ATTEMPTS
AMPLITUDE
```

---

## Best Practices

* Keep Ryujinx in the same position and size
* Do not move the window while running
* Use consistent camera angle
* Use clean templates
* Keep environment stable

---

## Quick Start

```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
python egg_bot.py
```

---

## Notes

This bot depends heavily on:

* template accuracy
* correct positioning
* stable emulator window
* proper controller configuration

If any of these are incorrect, the bot may not function properly.

---
