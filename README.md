# Table Tennis Ball Launcher & Practice Robot

An automated, microcontroller-based sports automation system designed to provide table tennis players with a reliable, repetitive training mechanism to build muscle memory without requiring a human partner. This project was developed as part of the **EE-222 Microprocessor Systems** course at the **National University of Sciences & Technology (NUST)**.

---

##  Project Overview

Manual feeding by a coach or partner can be inconsistent and fatiguing. This project solves that problem by utilizing an **ATmega328P** microcontroller to autonomously feed and shoot table tennis balls with continuous variable oscillation, democratizing high-level solo training.

The system bypasses high-level Arduino libraries to manipulate hardware registers directly in embedded C, demonstrating low-level control over PWM generation, timing delays, and motor driver orchestration.

### Key Features
* **Autonomous Operation:** Fully automated feeding, launching, and oscillation logic.
* **Dual-Motor Firing Mechanism:** Two DC motors spinning in opposite directions securely grip and shoot the ball.
* **Continuous Oscillation:** High-torque servo motors sweep from 0° to 180° and back to dynamically vary shot placement.
* **Register-Level Control:** Firmware written in pure embedded C via Atmel Studio for optimized hardware interaction.

---

##  Hardware Architecture & Components

The hardware isolates the high-discharge motor circuit from the logic circuit to ensure user safety and stable voltage levels.

| Component | Purpose | Selection Justification |
| :--- | :--- | :--- |
| **ATmega328P (Arduino UNO)** | Central Controller | Low cost, robust 16MHz clock, and direct register-level access via Atmel Studio. |
| **2 TT Gear Motors** | Ball Launcher | Spin simultaneously in opposite directions to tightly grip and launch the ball. |
| **BTS 7960 Motor Driver** | Dual H-Bridge Control | Safely handles the high current draw required by the physical TT motors. |
| **2 High-Torque Servos** | Actuation & Oscillation | Controls the ball feeder mechanism and the base oscillation for varied shot directions. |
| **Lithium-ion Batteries** | Power Supply | Provides stable, high-discharge energy directly to the motors, bypassing the MCU regulator. |

### System Logic Flow
1. **Power On / Start** $\rightarrow$ Initialize Timer0 (DC Motors) & Timer2 (Servo).
2. **Safety Delay** $\rightarrow$ Keep motors completely OFF for 500ms to allow safe player positioning.
3. **Engage Motors** $\rightarrow$ Drive launch motors continuously at a set PWM duty cycle.
4. **Autonomous Loop** $\rightarrow$ Sweep servo 0° to 180°, pause 1 second, sweep back 180° to 0°, pause 1 second, and repeat.

---

##  Technical Analysis & Calculations

### 1. PWM Frequency Calculation
To efficiently drive the small DC motors without losing torque or creating excessive switching heat, Timer0 is configured in **8-bit Fast PWM mode** with a prescaler of 64:

$$F_{PWM} = \frac{F_{CPU}}{\text{Prescaler} \times 256}$$

$$F_{PWM} = \frac{16,000,000}{64 \times 256} = 976.56 \text{ Hz}$$

### 2. Duty Cycle Configuration
The Output Compare Registers determine the average output voltage and motor speed:

$$\text{Duty Cycle (\%)} = \left( \frac{\text{OCRnx}}{255} \right) \times 100$$

* Setting `OCR0B = 150` yields an approximate **58% duty cycle** to maintain optimal continuous launch speed.

---

## 💻 Simulation & Implementation

The circuit architecture was fully modeled and simulated in **Proteus** prior to physical assembly to verify the microcontroller's autonomous PWM generation and servo sweeping logic. 

* **Software Stack:** Embedded C, Atmel Studio, Proteus Design Suite.
* **Hardware Frame:** Built utilizing a custom PVC tube guide system for reliable ball feeding and precise mechanical orientation.

---

## 👥 Team  Contributors

* **Alina Riaz** 
* **Muhammad Mutaal Khan** 
* **Muhammad Ahmed Saeed**
* **Ammar Bin Jalal** 


