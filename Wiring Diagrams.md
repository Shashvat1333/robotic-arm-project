**Robotics Arm Servo Wiring Diagram**
------------------------------------------------------------------------

<img width="675" height="537" alt="image" src="https://github.com/user-attachments/assets/9e5911ec-aa0e-417f-a0d2-205e02026b63" />

------------------------------------------------------------------------

| Component | ESP32 GPIO (Signal) | Power (+) | Ground (–) |
| --- | --- | --- | --- |
| Servo 1 – Base (DS3225MG) | GPIO 13 | Perfboard + line | Perfboard – line |
| Servo 2 – Shoulder (DS3225MG) | GPIO 12 | Perfboard + line | Perfboard – line |
| Servo 3 – Elbow (DS3225MG) | GPIO 14 | Perfboard + line | Perfboard – line |
| Servo 4 – Wrist Pitch (DS3225MG) | GPIO 27 | Perfboard + line | Perfboard – line |
| Servo 5 – Wrist Roll (MG90S) | GPIO 26 | Perfboard + line | Perfboard – line |
| Servo 6 – Gripper (MG90S) | GPIO 25 | Perfboard + line | Perfboard – line |
| ESP32 (board power, via fuse) | — | Perfboard + line → ESP32 5V/VIN pin | Perfboard – line → ESP32 GND pin |
| Perfboard + power line | — | 5V 10A Adapter (+) | — |
| Perfboard – ground line | — | — | 5V 10A Adapter (–) |

**How it flows:** The 5V 10A DC power supply connects directly to the custom soldered vertical bus lines on the perfboard, creating solid positive and negative rails. Every servo taps its power and ground straight into these soldered tracks. The ESP32 also bridges directly to these shared rails for its supply voltage and common ground, while individual signal wires run straight from each servo to their respective ESP32 GPIO pins.

------------------------------------------------------------------------
