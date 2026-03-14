# [cite_start]Tetris for NuMaker-PFM-M487 [cite: 9]

## 📌 Project Overview
[cite_start]This project is a classic Tetris game developed for the NuMaker-PFM-M487 development board[cite: 9]. [cite_start]It was created as the Group Project for the EEET2481|EEET2657 Embedded System Design and Implementation course[cite: 1, 3]. [cite_start]The goal of the project was to deliver a fully functional game with a clean graphical user interface (GUI), robust physical input handling, and highly optimized hardware drivers[cite: 10, 11]. 

## 🛠️ Hardware & Tools
* [cite_start]**Microcontroller:** NuMaker-PFM-M487 board [cite: 9]
* [cite_start]**Display:** ILI9341 LCD [cite: 9]
* [cite_start]**Input:** Hardware buttons and joystick [cite: 9]

## 🚀 Key Features
* [cite_start]**Complete Game Lifecycle:** Features a structured flow including a Welcome Screen, active Gameplay, Pause functionality, Game Over screen, and a High Score screen[cite: 7, 10]. 
* [cite_start]**Optimized Rendering:** Utilizes a custom hybrid rendering approach for smooth performance and low-latency gameplay[cite: 24].
* [cite_start]**Deterministic Speed Levels:** Implements hardware timers to manage block drop speeds, with verified waveform measurements for predictable difficulty scaling (e.g., speed levels 1, 5, and 10)[cite: 35, 36, 37, 38].
* [cite_start]**Robust Input Handling:** Deterministic tick and debounce management ensures responsive and accurate movement[cite: 33, 34].

## 🏗️ Software Architecture
[cite_start]The codebase is highly modular to simplify testing and debugging:
* [cite_start]**BSP & Drivers (`EBI_LCD_Module.c`):** Handles low-level initialization for the LCD, GPIOs, timers, and direct pixel writing[cite: 26].
* [cite_start]**Display Layer (`UIDesign.c`, `WelcomeScreen.c`, etc.):** Responsible for drawing static bitmaps, mapping game tiles to pixel rectangles, and executing partial-redraw logic[cite: 27].
* [cite_start]**Game Logic (`LogicGame.c`):** The deterministic engine that handles spawning, moving, rotating blocks, and calculating scores[cite: 28].
* [cite_start]**Control & FSM:** Uses interrupts (ISRs) and a Finite State Machine to control transitions between WELCOME, RUNNING, PAUSED, and GAME OVER states[cite: 29].

## 🧠 Design Choices & Optimizations
### The "Hybrid" UI Approach
[cite_start]Initially, the GUI was planned using AppWizard[cite: 12]. [cite_start]However, while AppWizard is excellent for managing static screens, it expects to manage the entire GUI lifecycle, making it inefficient for the frequent, per-tile pixel updates required by Tetris[cite: 15, 16]. 

[cite_start]To achieve smooth gameplay, we implemented a **hybrid rendering approach**[cite: 22]:
* [cite_start]**Static Assets:** UI elements and backgrounds were designed in AppWizard, exported as raw RGB565 bitmap arrays, and stored as static resources in the firmware[cite: 22].
* [cite_start]**Dynamic Rendering:** The actual gameplay uses direct EBI writes to the ILI9341 LCD for dynamic scenes[cite: 13, 23]. 

**Benefits of this tradeoff:**
* [cite_start]Enabled highly efficient partial updates (only redrawing changed tiles)[cite: 19].
* [cite_start]Simplified timer and ISR interactions by controlling exactly when pixel bursts happen[cite: 20].
* [cite_start]Provided predictable timing, responsive input, and smooth rendering[cite: 34].

## 👥 Authors
* [cite_start]**Truong Kiem Minh** (s4067934) [cite: 4]
* [cite_start]**Tran Nguyen Bao Hoc** (s4038330) [cite: 4]
