Robotic Arm Project Journal
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 1**: July 11, 2026


Time spent: **2 hours**


**What I worked on**

Started planning my robotic arm project today. I focused mainly on research, understanding the requirements, and making early design decisions before doing anything else.

I researched the fundamentals of degrees of freedom (DOF) and compared different robotic arm designs with 3, 4, 5, and 6 DOF. More DOF allows greater control over the end effector's position and orientation, but it also increases complexity, cost, programming difficulty, and possible error buildup because small inaccuracies in each joint can affect the final position.

Based on my initial research, I am currently planning to build a 6 DOF robotic arm because it provides more flexibility and allows the arm to perform more complex movements. However, I will confirm this decision after completing more mechanical design research and torque calculations.


**What I learned**

I learned about the difference between open-loop and closed-loop servos. Closed-loop servos use position feedback from sensors such as encoders, which improves accuracy and reduces positioning errors across multiple joints. However, they are significantly more expensive. Since my planned payload is light, less than 500g, I am currently considering open-loop PWM servos as a better balance between cost and performance for a first robotic arm.

I researched how servo torque requirements change depending on the location of the joint. Joints closer to the base require more torque because they support the weight of the entire arm, while joints farther away require less torque. My current plan is to investigate using higher-torque servos, such as the MG996R, for major joints like the base, shoulder, elbow, and wrist. Lower torque servos such as the MG90S may be better suited for lighter joints like wrist rotation and the gripper.

I compared Arduino and ESP32 as possible controllers. I am currently leaning toward using an ESP32 because it includes built-in WiFi, which would allow me to control the robotic arm remotely through a phone-based interface. I also learned that the ESP32 uses 3.3V logic and may require different libraries compared to Arduino boards, such as ESP32Servo.h.

I learned that multiple servos cannot be powered directly from a microcontroller because they can draw more current than the board can provide. A separate power supply will likely be needed for the servos, with a shared ground connection between the power supply and the ESP32.

I researched possible materials for the robotic arm frame. PLA is currently my preferred option because it is affordable, easy to print, and should be strong enough for an initial lightweight prototype. I will continue researching whether stronger materials or different printing settings are needed for areas experiencing higher stress.


**Decisions made**

My current design direction is a 6 DOF robotic arm, although this may change after.

I am currently considering open-loop PWM servos because they provide a better balance between cost and performance for this project.

I am planning to compare MG996R and MG90S servo combinations depending on the torque requirements of each joint.

I am planning to use an ESP32 as the main controller because of its built-in WiFi capabilities.

I am planning to use an external power supply for the servos instead of powering them directly from the controller.

I am considering PLA for the frame.


**Questions to investigate**

Are the selected servos strong enough for the planned arm length and payload?

Will PLA provide sufficient strength for the highest-stress joints?

Should I use bearings or other mechanical supports to reduce friction?

How can I reduce servo vibration and backlash?

Is a 6 DOF design practical for my first robotic arm build?


**Next steps**

Create a detailed Bill of Materials with estimated prices.

Research servo specifications and calculate torque requirements.

Begin initial CAD sketches for the arm structure.

Decide the final joint layout and servo placement.

Compare existing open-source robotic arms for design inspiration.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
