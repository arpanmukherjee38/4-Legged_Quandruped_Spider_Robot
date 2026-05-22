# 🕷️ Bluetooth-Enabled 3D Printed Quadruped Spider Robot

![Arduino](https://img.shields.io/badge/Arduino-Nano-00979D?style=flat&logo=arduino&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)
![Status](https://img.shields.io/badge/Status-Prototype%20Complete-brightgreen?style=flat)
![Conference](https://img.shields.io/badge/Presented%20at-TSSC%202026-blue?style=flat)

A low-cost, 3D-printed quadruped spider robot built on Arduino Nano with 12 SG90 servo motors, Bluetooth wireless control, and ultrasonic obstacle detection. Designed for search and rescue applications, educational demonstrations, and as a research prototype platform for legged locomotion.

> **Presented at:** 1st International Conference on Transformative Social Sciences (TSSC 2026), UEM Kolkata, Feb. 06, 2026.

---

## Demo

<img width="3072" height="4096" alt="WhatsApp Image 2026-05-13 at 10 32 51 PM" src="https://github.com/user-attachments/assets/c6daea54-58db-48c1-bc28-4c5b78db135f" />


## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Hardware Components](#hardware-components)
- [System Architecture](#system-architecture)
- [Gait Planning & Control](#gait-planning--control)
- [Movement Capabilities](#movement-capabilities)
- [Results](#results)
- [Getting Started](#getting-started)
- [Future Scope](#future-scope)
- [Applications](#applications)
- [Team](#team)
- [References](#references)

---

## Overview

This project addresses the need for **simple, affordable quadruped robotic platforms** that support hands-on learning, prototyping, and experimentation in embedded systems and legged locomotion. Unlike most high-cost quadruped robots that rely on complex control algorithms and high computational resources, this robot achieves stable multi-terrain locomotion using a heuristic, iterative servo-tuning approach — no inverse kinematics required.

The robot features:
- A **bio-inspired spider-leg design** (Coxa–Femur–Tibia per leg)
- **3 degrees of freedom per leg** (12 servos total)
- **Wireless Bluetooth control** for remote operation
- **Ultrasonic obstacle detection** for reactive navigation

---

## Features

- ✅ Stable walking on flat and uneven terrains
- ✅ Symmetric gait sequencing without complex kinematics
- ✅ Bluetooth-based wireless remote control
- ✅ Real-time ultrasonic obstacle avoidance
- ✅ Multiple motion modes (walk, crawl, sit, dance, handshake)
- ✅ Modular, 3D-printed frame — easy to repair and customize
- ✅ Low-power Arduino Nano microcontroller
- ✅ Expandable architecture for AI/sensor upgrades

---

## Hardware Components

| Component | Specification | Quantity |
|---|---|---|
| Microcontroller | Arduino Nano | 1 |
| Servo Motors | SG90 (180°) | 12 |
| Distance Sensor | HC-SR04 Ultrasonic | 1 |
| Wireless Module | HC-05 Bluetooth | 1 |
| Power Supply | SMPS 5V | 1 |
| Frame | 3D Printed PLA Parts | — |
| Misc | Jumper wires, connectors | — |

---

## System Architecture

Each leg follows the spider anatomy model with three servo-controlled joints:

```
Spider Body
├── Front-Right (FR) Leg  →  Servo1 (Z-axis) | Servo2 (Y-axis) | Servo3 (Y-axis)
├── Front-Left  (FL) Leg  →  Servo4           | Servo5           | Servo6
├── Back-Right  (BR) Leg  →  Servo7           | Servo8           | Servo9
└── Back-Left   (BL) Leg  →  Servo10          | Servo11          | Servo12
```

- **FR & BL legs** share identical angular orientations (diagonal pair)
- **FL & BR legs** move concomitantly (opposite diagonal pair)
- All servos calibrated to a neutral position of **θ = 90°**

**Control Flow:**
```
Bluetooth Input → Arduino Nano → Servo PWM Signals → Leg Motion
                               ↑
               HC-SR04 Ultrasonic Sensor (obstacle feedback)
```

---

## Gait Planning & Control

The robot uses a **bio-inspired trot-like gait** with independent phase control for each leg:

1. **Lift Phase** — Leg raised off the ground
2. **Swing Phase** — Leg moved forward through air
3. **Stance Phase** — Leg planted, body propelled forward

Servo angles are fine-tuned using **iterative heuristic calibration** (trial-and-error testing), avoiding computationally expensive algorithms like inverse kinematics. This makes the system deployable on low-power hardware without sacrificing locomotion stability.

---

## Movement Capabilities

| Motion | Description |
|---|---|
| Forward Walk | Standard trot gait, stable on flat and uneven surfaces |
| Backward Walk | Reverse gait sequence |
| Left / Right Turn | Differential leg speed for directional steering |
| Crawl | Low-clearance motion for confined spaces |
| Sit | Folds legs into a resting pose |
| Dance | Rhythmic coordinated leg movements |
| Handshake | Single leg raise gesture |

---

## Results

- **Multi-terrain locomotion** achieved with minimal body oscillation on flat and slightly uneven surfaces
- **Symmetric gait** maintained balance without complex optimization
- **Directional control** (forward, backward, turning) validated via Bluetooth commands
- **Obstacle detection** loop confirmed — robot halts/redirects before collision

---

## Getting Started

### Prerequisites

- [Arduino IDE](https://www.arduino.cc/en/software) (v1.8+ or v2.x)
- Arduino `Servo.h` library (built-in)

### Wiring

1. Connect all 12 SG90 servos to Arduino Nano PWM pins (D2–D13)
2. Connect HC-SR04 `Trig` → D14 (A0), `Echo` → D15 (A1)
3. Connect HC-05 `TX` → D0 (RX), `RX` → D1 (TX)
4. Power servos via external 5V SMPS (do **not** power from Arduino 5V pin)

### Upload

```bash
git clone https://github.com/<your-username>/quadruped-spider-robot.git
cd quadruped-spider-robot
# Open quadruped_main.ino in Arduino IDE
# Select Board: Arduino Nano | Processor: ATmega328P
# Upload
```

### Bluetooth Control

Pair your phone to the **HC-05** module (default PIN: `1234`). Use any serial Bluetooth terminal app and send the following commands:

| Command | Action |
|---|---|
| `F` | Forward |
| `B` | Backward |
| `L` | Turn Left |
| `R` | Turn Right |
| `S` | Stop / Stand |
| `C` | Crawl |
| `D` | Dance |
| `H` | Handshake |

---

## Future Scope

- [ ] Full wireless directional control integration
- [ ] IMU-based terrain-adaptive gait correction
- [ ] AI/ML-based autonomous navigation
- [ ] Camera module for visual obstacle recognition
- [ ] ROS integration for advanced path planning
- [ ] Energy harvesting for extended runtime

---

## Applications

- 🔍 **Search & Rescue** — Navigate rubble and uneven terrain in disaster zones
- 📡 **Surveillance** — Remote monitoring in restricted or hazardous areas
- 🎓 **Education** — Hands-on platform for servo control, gait mechanics, and embedded systems
- 🔬 **Research** — Prototype base for testing locomotion algorithms and sensors
- 🎪 **Demonstration** — Exhibitions and robotics showcases

---

## Team

**Supervisors:**
- Dr. Soumyendu Banerjee *(Principal Investigator)*
- Dr. Sanjay Bhadra *(Co-Investigator)*

**Members** — Dept. of Robotics & AI, 2024 Batch:

| Name | Roll No. | Enrollment No. |
|---|---|---|
| Arpan Mukherjee | 11 | 12024002038010 |
| Rupsa Saha | 43 | 12024002038042 |
| Priyanshu Das | 26 | 12024002038025 |
| Ishika Patra | 59 | 12024002038058 |
| Atri Ghosh | 57 | 12024002038056 |
| Mousumi Bera | 55 | 12024002038054 |

**Paper Code:** PROJRAI481

---

## Citation

If you use this project in your research or work, please cite:

```bibtex
@inproceedings{banerjee2026quadruped,
  author    = {S. Banerjee and A. Ghosh and S. Bhadra and R. Saha and P. Das and A. Mukherjee},
  title     = {Bluetooth-Enabled 3D Printed Quadruped Spider Robot on Arduino Nano:
               A Socio-Technical Study Bridging Indian Knowledge Frameworks and Community Empowerment},
  booktitle = {1st International Conference on Transformative Social Sciences (TSSC 2026):
               Bharat's Wisdom for Global Solutions},
  year      = {2026},
  month     = {February},
  note      = {Hybrid Mode, UEM Kolkata}
}
```

---

## References

1. Rahman et al., "A Dynamic Approach to Low-Cost Design of a 12-DoF Quadruped Robot," *Robotics*, 2023.
2. Nguyen et al., "Adaptive Gait Control for Quadruped Robots on Varied Slopes via ARS Algorithm," 2025.
3. Hoang et al., "Path Tracking Controller of Quadruped Robot for Obstacle Avoidance Using Potential Functions Method," 2024.
4. Majithia et al., "Design, Motions, Capabilities, and Applications of Quadruped Robots: A Comprehensive Review," *Front. Mech. Eng.*, 2024.
5. Meng et al., "Trot Gait Stability Control of Small Quadruped Robot Based on MPC and ZMP Methods," *Processes*, 2023.

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
