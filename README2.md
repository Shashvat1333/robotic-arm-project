# Robotic Arm Project

[![View Wiring Documentation](https://img.shields.io/badge/Wiring-Documentation-blue)](Wiring%20Diagrams.md)

A custom-designed, multi-axis robotic arm controlled wirelessly via Bluetooth using an ESP32 and Bluepad32.

![Robotic Arm Render](https://github.com/user-attachments/assets/e9d09f8e-5ce9-402f-af84-5a91fc626033)

## Overview
This project combines mechanical engineering, 3D printing, electronics, and embedded firmware development. The goal is to build a fully articulated, functional robotic arm with multiple degrees of freedom controlled wirelessly.

### Features:
- Custom mechanical parts, linkages, and gear assemblies designed with precise tolerances for 3D printing.
- Wireless control integration using an ESP32 and Bluepad32 library.
- Custom power distribution using a high-current 5V 10A DC supply and soldered perfboard bus lines to handle high servo loads safely.

---

## CAD Model & Assembly
The mechanical assembly and individual parts were designed in Onshape and optimized for 3D printing with proper clearance tolerances. 
- All production-ready parts and full assemblies are stored in the `cad/` folder as `.step` files.

![CAD Assembly View](https://github.com/user-attachments/assets/6f530a01-1f68-40d2-a437-52708d4fa79e)

---

## Schematic & Wiring
Because this project utilizes modular components wired together on a custom soldered perfboard rather than a manufactured PCB, the system relies on a detailed wiring layout. 

You can view the full connection specifications in [Wiring Diagrams.md](Wiring%20Diagrams.md).

| Component | ESP32 GPIO (Signal) | Power (+) | Ground (–) |
|---|---|---|---|
| Servo 1 – Base (DS3225MG) | GPIO 21 | Perfboard + bus line | Perfboard – bus line |
| Servo 2 – Shoulder (DS3225MG) | GPIO 5 | Perfboard + bus line | Perfboard – bus line |
| Servo 3 – Elbow (DS3225MG) | GPIO 18 | Perfboard + bus line | Perfboard – bus line |
| Servo 4 – Wrist Pitch (DS3225MG) | GPIO 19 | Perfboard + bus line | Perfboard – bus line |
| Servo 5 – Wrist Roll (MG90S) | GPIO 4 | Perfboard + bus line | Perfboard – bus line |
| Servo 6 – Gripper (MG90S) | GPIO 22 | Perfboard + bus line | Perfboard – bus line |
| ESP32 NodeMCU Board | — | VIN pin connected to + bus | GND pin connected to – bus |
| Power Supply | — | 5V 10A DC Adapter (+) | 5V 10A DC Adapter (–) |

---

## Firmware
The control firmware is written in C++ using the Arduino framework, utilizing the `ESP32Servo` and `Bluepad32` libraries to map game controller joysticks and buttons to the servos. 
- The source code is located at `firmware/firmware.ino`.

---

## Bill of Materials (BOM)

| Item | Quantity | Description |
| :--- | :--- | :--- |
| ESP32 NodeMCU | 1x | Main microcontroller board |
| DS3225MG Servo Motors | 4x | High-torque joint actuation (Base, Shoulder, Elbow, Wrist Pitch) |
| MG90S Micro Servos | 2x | Wrist roll and gripper control |
| 5V 10A DC Power Adapter | 1x | External high-current power supply |
| Perfboard & Hookup Wire | Set | Custom soldered power distribution bus |
| 3D Printed Parts | Set | PETG/PLA structural and mechanical components |
| Fasteners & Hardware | Assorted | M3 bolts and heat-set inserts |
