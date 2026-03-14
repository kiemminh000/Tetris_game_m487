# [cite_start]Tetris for NuMaker-PFM-M487 [cite: 9]

## 📌 Project Overview
This project is a classic Tetris game developed for the NuMaker-PFM-M487 development board. It was created as the Group Project for the EEET2481|EEET2657 Embedded System Design and Implementation course. The goal of the project was to deliver a fully functional game with a clean graphical user interface (GUI), robust physical input handling, and highly optimized hardware drivers. 

## 🛠️ Hardware & Tools
* **Microcontroller:** NuMaker-PFM-M487 board 
* **Display:** ILI9341 LCD 
* **Input:** Hardware buttons and joystick 

## 🚀 Key Features
* ]**Complete Game Lifecycle:** Features a structured flow including a Welcome Screen, active Gameplay, Pause functionality, Game Over screen, and a High Score screen. 
* **Optimized Rendering:** Utilizes a custom hybrid rendering approach for smooth performance and low-latency gameplay.
* **Deterministic Speed Levels:** Implements hardware timers to manage block drop speeds, with verified waveform measurements for predictable difficulty scaling (e.g., speed levels 1, 5, and 10).
* **Robust Input Handling:** Deterministic tick and debounce management ensures responsive and accurate movement.

## 🏗️ Software Architecture
The codebase is highly modular to simplify testing and debugging:
* **BSP & Drivers (`EBI_LCD_Module.c`):** Handles low-level initialization for the LCD, GPIOs, timers, and direct pixel writing.
* **Display Layer (`UIDesign.c`, `WelcomeScreen.c`, etc.):** Responsible for drawing static bitmaps, mapping game tiles to pixel rectangles, and executing partial-redraw logic.
* **Game Logic (`LogicGame.c`):** The deterministic engine that handles spawning, moving, rotating blocks, and calculating scores.
* **Control & FSM:** Uses interrupts (ISRs) and a Finite State Machine to control transitions between WELCOME, RUNNING, PAUSED, and GAME OVER states.

## 🧠 Design Choices & Optimizations
### The "Hybrid" UI Approach
Initially, the GUI was planned using AppWizard. However, while AppWizard is excellent for managing static screens, it expects to manage the entire GUI lifecycle, making it inefficient for the frequent, per-tile pixel updates required by Tetris. 

To achieve smooth gameplay, we implemented a **hybrid rendering approach**:
* **Static Assets:** UI elements and backgrounds were designed in AppWizard, exported as raw RGB565 bitmap arrays, and stored as static resources in the firmware.
* **Dynamic Rendering:** The actual gameplay uses direct EBI writes to the ILI9341 LCD for dynamic scenes. 

**Benefits of this tradeoff:**
* Enabled highly efficient partial updates (only redrawing changed tiles).
* Simplified timer and ISR interactions by controlling exactly when pixel bursts happen.
* Provided predictable timing, responsive input, and smooth rendering.

## 👥 Authors
* **Truong Kiem Minh** (s4067934) 
* **Tran Nguyen Bao Hoc** (s4038330) 
