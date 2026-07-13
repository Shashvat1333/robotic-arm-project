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

**Day 2**: July 12, 2026


Time spent: **2.5 hours**


**What I worked on**

Focused today on refining the torque calculations for the robotic arm and updating my preliminary Bill of Materials (BOM).

Using my planned arm length of approximately 42 cm, I recalculated the shoulder torque requirements with a realistic payload of 100 g, which is the maximum weight I currently expect the arm to lift. I estimated the total weight beyond the shoulder joint, including the elbow, wrist, gripper servos, the printed structure, and the payload, then calculated the required torque at full horizontal extension.


**What I learned**

Using a 42 cm arm length and a 100 g payload, I calculated that the shoulder joint would require approximately 15.4 kg·cm of torque. This is beyond what a standard MG996R servo, rated at roughly 11–13 kg·cm, can reliably provide with a comfortable safety margin. Based on these calculations, the base and shoulder joints require higher-torque servos.

I researched higher-torque servo options and selected the HOOYIJ DS3230MG as my current choice for the base and shoulder joints. According to the manufacturer's specifications, it provides approximately 29.5 kg·cm at 5 V and up to 34.5 kg·cm at 6.8 V, giving a comfortable safety margin for my current design.

My current planned servo configuration is:

2 × HOOYIJ DS3230MG for the base and shoulder

2 × Deegoo MG996R for the elbow and wrist pitch

2 × MG90S for the wrist roll and gripper

Based on my calculations, the MG90S servos appear suitable for the wrist roll and gripper because these joints have a much shorter lever arm of approximately 5–8 cm. The estimated torque requirement is about 0.84 kg·cm, which is well below the servo's rated torque.

I learned that servo movement can be limited in software using the `constrain()` function before sending a position command. Although the DS3230MG supports approximately 270° of rotation, I currently plan to limit it to 180° because the extra range is not required for this design.

I researched bearing-supported joints, including two-sided U-mount brackets, as a way to reduce the structural load placed on servo output shafts. Because this is a lightweight prototype, I currently plan to build without them and evaluate whether they are needed after testing.

I also reviewed the expected power requirements. Although all six servos are unlikely to stall simultaneously during normal operation, the theoretical worst-case current draw could reach approximately 9–13 A. Based on this, I updated my planned power supply from a 5 V 6 A adapter to a 5 V 10 A (50 W) power supply to provide additional headroom.

I watched several videos of existing robotic arm projects to study different design approaches and gather ideas for my own build. I paid particular attention to joint layouts, servo placement, bracket design, wire management, and overall mechanical structure. This helped me identify features that may be useful to incorporate into my own design while avoiding common design issues.


**Decisions made**

My current planned servo configuration consists of two DS3230MG servos for the base and shoulder, two MG996R servos for the elbow and wrist pitch, and two MG90S servos for the wrist roll and gripper.

I set my design payload target to approximately 100 g because it better reflects the lightweight objects I intend the robotic arm to manipulate.

I selected a 5 V 10 A BTF-LIGHTING power supply instead of the originally planned 6 A version.

I added M3 heat-set inserts and an M3 screw kit to the preliminary Bill of Materials for mounting servos and brackets into PLA components.

I also added one 1 kg spool of Elegoo PLA filament to the Bill of Materials.


**Next steps**

Begin designing the robotic arm frame in CAD using the planned dimensions and selected servo sizes.

Design the joint brackets and servo mounts to accommodate M3 heat-set inserts.

Verify the servo placement, clearances, and range of motion within the CAD assembly before printing the prototype.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 3**: July 13, 2026


**Time spent**: 4 hours 30 minutes


**What I worked on**

Started the CAD design for the robotic arm today, focusing on the base and shoulder assembly. Most of my time was spent designing and understanding the gear system for the base because I wanted to achieve a full 360° rotation using a 270° positional servo instead of switching to a continuous rotation servo or adding a slip ring.


**What I learned**

I worked through the relationship between gear ratios and rotational movement. To achieve 360° of platform rotation from a servo capable of rotating 270°, I calculated that a 3:4 step-up gear ratio would provide the required motion.

I learned that gears must have the same module to mesh correctly. Matching the overall diameter alone is not enough because the tooth size and spacing must also be identical.

During the design process, I discovered that my initial gear sizes of 6 and 8 teeth were too small and would not mesh properly due to interference between the teeth. To solve this, I increased the gear sizes to 18 and 24 teeth while maintaining the same 3:4 ratio, resulting in a much more practical gear set.

I used Onshape's Spur Gear FeatureScript to generate accurate involute gears instead of drawing the tooth profiles manually. I also learned how to use the Boolean Union tool to combine multiple solid bodies into a single part.

While working in the assembly environment, I learned how to use Revolute Mates to define rotational motion and Gear Relations to link two gears together so they rotate correctly relative to one another.

I also learned about backlash in 3D-printed gears. Even when the CAD model is mathematically correct, printing tolerances can cause gears to bind if there is no clearance. Because of this, I researched how small adjustments to the center distance can improve gear performance.

For my current 18-tooth and 24-tooth gear set with a module of 1.5, the calculated center distance is 31.5 mm. I currently plan to increase this slightly to approximately 31.7–31.8 mm to account for FDM printing tolerances and reduce the likelihood of binding.

I also watched several videos demonstrating gear design and robotic arm mechanisms. These helped me better understand practical gear layouts, assembly techniques, and common design considerations before continuing with my own CAD model.


**Decisions made**

My current design uses a 270° DS3230MG servo with a 3:4 step-up gear ratio to achieve approximately 360° of base rotation.

My current gear design uses an 18-tooth driving gear and a 24-tooth driven gear with a module of 1.5.

I currently plan to use a center distance of approximately 31.7–31.8 mm to provide additional clearance for 3D printing.

Based on my current torque calculations, the reduction in output torque caused by the gear ratio remains acceptable for my planned payload.


**Next steps**

Finish the CAD design for the base gear housing and rotating platform.

Print and test the gear pair to verify that the selected center distance provides smooth rotation without excessive backlash or binding.

Continue designing the shoulder joint once the base gear system has been validated.

Begin the CAD design for the elbow and wrist assemblies.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
