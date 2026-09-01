# Robotic Arm Project

[![View Wiring Documentation](https://img.shields.io/badge/Wiring-Documentation-blue)](Wiring%20Diagrams.md)

A custom-designed, multi-axis robotic arm controlled wirelessly via Bluetooth using an ESP32 and Bluepad32.

![Robotic Arm Render](https://github.com/user-attachments/assets/e9d09f8e-5ce9-402f-af84-5a91fc626033)

## Overview
This project combines mechanical engineering, 3D printing, electronics design, and embedded firmware development into a cohesive hardware system. The primary goal is to build a fully articulated, functional robotic arm with multiple degrees of freedom that responds seamlessly to a wireless game controller. By integrating custom gear assemblies, iterative 3D-printed brackets, and robust power management, this project bridges the gap between digital design and physical prototyping.

### Key Features:
- **Custom Mechanical Design:** Engineered with precise tolerance margins for 3D printing, featuring custom gear trains and linkage assemblies designed in Onshape.
- **Wireless Control Integration:** Utilizes an ESP32 microcontroller paired with the Bluepad32 framework to read live joystick and button inputs from a standard Bluetooth controller.
- **Safe Power Distribution:** Employs a dedicated 5V 10A DC power supply routed through custom soldered bus lines on a perfboard, replacing high-resistance plastic breadboards to handle heavy servo current draws safely.

---

## CAD Model & Assembly
The structural framework and mechanical joints of the robotic arm were modeled with close attention to mechanical clearances and structural integrity. To support open-source collaboration and manufacturing, all production-ready parts and full assemblies are stored directly in the `cad/` folder as `.step` files. 

https://github.com/user-attachments/assets/6f530a01-1f68-40d2-a437-52708d4fa79e

---

## Schematic & Wiring
Because this project utilizes modular components wired together on a custom soldered perfboard rather than a manufactured printed circuit board, the system relies on a detailed wiring layout. 

You can view the complete connection specifications and documentation in [Wiring Diagrams.md](Wiring%20Diagrams.md).

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
The control firmware is written in C++ using the Arduino framework, integrating the `ESP32Servo` and `Bluepad32` libraries to map controller joysticks and triggers directly to servo positions. 
- The complete source code is located [here](https://github.com/Shashvat1333/robotic-arm-project/blob/main/FIRMWARE.ino).

---

## Bill of Materials (BOM)

| # | Item | Qty | Description | Price (tax incl.) | Link |
|---|------|-----|-------------|-------------------|------|
| 1 | 25KG Digital RC Servo (DS3225) | 4 Pack | Waterproof, high-torque servo for main arm joints | $65.60 | [AliExpress](https://www.aliexpress.com/item/1005009734701047.html) |
| 2 | MG90S 9g Micro Servo Motor | 2 Pack | Small servo for gripper / wrist actuation | $7.40 | [AliExpress](https://www.aliexpress.com/item/4000903254039.html) |
| 3 | 5V 10A Power Supply Adapter | 1 | Main power supply for servos | $23.40 | [AliExpress](https://www.aliexpress.com/item/1005004121728138.html) |
| 4 | 5.5x2.1mm DC Power Female Jack Pigtail | 1 | Connects power adapter to circuit | $6.00 | [AliExpress](https://www.aliexpress.com/item/1005008401380227.html) |
| 5 | ESP32-WROOM-32 Dev Board (CH340C, Type-C) | 1 | Dual-core WiFi + Bluetooth MCU for arm control (Bluepad32) | $8.00 | [AliExpress](https://www.aliexpress.com/item/1005008981904299.html) |
| 6 | 22AWG Stranded Wire | 1 | Flexible wiring for all connections, including servo leads | $10.17 | [AliExpress](https://www.aliexpress.com/item/1005006441248773.html) |
| 7 | KADRICK 420PCS M3 Heat Set Inserts Kit | 1 | Threaded inserts for 3D-printed parts | $25.48 | [Amazon](https://www.amazon.com/Threaded-Assortment-M3x6-30mm-Installation-Printing/dp/B0GYRQG7F2/) |
| 8 | Perfboard (6cm × 8cm) | 1 | Solder-based board — replaces breadboard for safe high-current servo wiring | $2.80 | [AliExpress](https://www.aliexpress.com/item/1005006829112244.html) |
| 9 | PLA+ Filament 1.75mm 1KG | 673g used | 3D printing material for arm structural parts — cost reflects grams actually used (sliced in PrusaSlicer), not full spool purchased | $15.07 | [AliExpress](https://www.aliexpress.com/item/1005011683191901.html) |
| 10 | Import Charges | — | Customs/import fees on international orders | $12.00 | — |

**Total Project Cost: $175.92**
