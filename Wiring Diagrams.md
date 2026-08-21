**Robotics Arm Servo Wiring Diagram**
------------------------------------------------------------------------

<img width="756" height="636" alt="image" src="https://github.com/user-attachments/assets/496f8156-4339-448f-bdc7-95d723538667" />

------------------------------------------------------------------------

| Component | ESP32 GPIO (Signal) | Power (+) | Ground (–) |
|---|---|---|---|
| Servo 1 – Base (DS3225MG) | GPIO 13 | Breadboard + rail | Breadboard – rail |
| Servo 2 – Shoulder (DS3225MG) | GPIO 12 | Breadboard + rail | Breadboard – rail |
| Servo 3 – Elbow (DS3225MG) | GPIO 14 | Breadboard + rail | Breadboard – rail |
| Servo 4 – Wrist Pitch (DS3225MG) | GPIO 27 | Breadboard + rail | Breadboard – rail |
| Servo 5 – Wrist Roll (MG90S) | GPIO 26 | Breadboard + rail | Breadboard – rail |
| Servo 6 – Gripper (MG90S) | GPIO 25 | Breadboard + rail | Breadboard – rail |
| ESP32 (board power, via fuse) | — | Breadboard + rail → ESP32 5V/VIN pin | Breadboard – rail → ESP32 GND pin |
| Breadboard + rail | — | 5V 10A Adapter (+) | — |
| Breadboard – rail | — | — | 5V 10A Adapter (–) |

**How it flows:** the 5V 10A adapter feeds the breadboard's + and – power rails directly. Every servo's red wire taps into the + rail, and every servo's brown/black wire taps into the – rail. The ESP32 also grounds into that same – rail (GND pin), and its power comes off the + rail into VIN — this shared rail is what ties the whole system to one common ground.

Each servo's signal (orange/yellow) wire skips the breadboard rails entirely and runs as a direct jumper wire straight to its assigned GPIO pin.

------------------------------------------------------------------------
