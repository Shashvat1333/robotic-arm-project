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


Time spent: **4 hours 30 minutes**


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

**Day 4**: July 14, 2026


Time spent: **3 hours**


**What I worked on**

Continued working on the CAD design and preparing the model for 3D printing. Most of today's work focused on researching tolerances and print settings for small, high-stress features such as gear teeth, heat-set insert holes, and press-fit joints. By the end of today's session, I estimate the CAD design is approximately 75% complete.


**What I learned**

I researched recommended clearances for different types of fits used in 3D printing. A clearance of approximately 0.1 mm is commonly recommended for press-fit parts, while 0.2–0.3 mm provides a smoother moving fit and 0.4–0.5 mm creates a looser fit. Using clearances that are too small can cause parts to fuse together or become difficult to assemble after printing.

I learned how to size holes for M3 heat-set inserts. Based on the insert dimensions I plan to use, the hole should be approximately 0.1 mm larger than the measured outer diameter of the insert, with about 0.5 mm of additional depth so the insert can sit flush once installed.

I researched proper techniques for installing heat-set inserts using a soldering iron. Maintaining a temperature of approximately 200–220°C and applying steady downward pressure helps produce a cleaner installation. I also learned that excessive movement while removing the soldering iron or using an undersized hole can cause excess plastic to build up around the insert instead of leaving a clean, flush surface.

I compared manually adjusting dimensions in CAD with using a slicer's hole compensation feature. Based on my research and the printer I plan to use, I currently intend to make dimensional adjustments directly in the CAD model because it provides more consistent and predictable results.

I also researched print settings for small, detailed parts such as gears and servo brackets. Based on the recommendations I found, I currently plan to use a layer height of 0.16 mm with 3–4 wall loops to provide a good balance between print quality and part strength.


**Decisions made**

I plan to standardize the clearances used throughout the CAD model based on the type of fit required for each part.

I plan to model all M3 heat-set insert holes using the insert's measured outer diameter plus approximately 0.1 mm, along with an additional 0.5 mm of depth.

I currently plan to make dimensional adjustments directly in the CAD model instead of relying on slicer hole compensation.

My planned print settings for small, high-stress components are a 0.16 mm layer height with 3–4 wall loops.

Next steps

Finish up %100 of the base and shoulder parts.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 5**: July 15, 2026


Time spent: **2 hours**


**What I worked on**

Continued working on the CAD design for the robotic arm. Today's focus was on completing the base and shoulder components and beginning the assembly to better visualize how the individual parts fit together. Creating the assembly also helped me identify potential alignment issues and areas that may need adjustment before printing.


**What I learned**

I learned that it is important to verify design decisions against the manufacturer's recommendations instead of relying solely on general guidelines. After reviewing the specifications for the heat-set inserts I plan to use with PLA, I reduced the insert hole diameter from 4.6 mm to 4.4 mm to better match the recommended dimensions.

Working with the assembly also gave me a better understanding of how the different components interact. Being able to see the parts together made it easier to identify areas that could interfere with movement or require additional clearance before manufacturing.

While reviewing the completed parts, I also looked for potential weak points in the design. I added fillets to reduce stress concentrations around sharp corners and increased the thickness of several features that appeared likely to experience higher loads. Making these improvements during the design stage should help reduce the likelihood of failures or redesigns later in the project.


**Decisions made**

Completed the CAD design for the base and shoulder components.

Began creating the full assembly to verify part placement and overall fit.

Updated the M3 heat-set insert hole diameter from 4.6 mm to 4.4 mm based on the manufacturer's recommendations for PLA.

Added fillets and reinforced several areas of the design to improve strength before printing.


**Next steps**

Continue building the full CAD assembly and verify that all components fit together correctly.

Review the remaining parts for any additional weak points or areas that could benefit from reinforcement.

Complete the remaining CAD components.


<img width="532" height="653" alt="image" src="https://github.com/user-attachments/assets/c359f7c1-f972-4ee5-9dc3-7ed324049b32" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 6**: July 16, 2026


Time spent: **5 hours**


**What I worked on**

Today I continued working on the CAD design for my robotic arm. I finished designing the shoulder arm and made several improvements to the base and shoulder components to strengthen the design and improve how the parts fit together.

I also decided to use standard 25T servo arms for connecting the arm sections. To prepare for assembly, I created simple CAD models of the DS3230MG servo and a standard 25T servo arm. I then added these parts into the assembly to better visualize how the components would connect and move together.


**What I learned**

Today I learned more about the exact mounting specifications of the DS3230MG servo and its servo arm connection. I found the manufacturer's dimensions for the servo arm mounting pattern, which specifies a 25T, 5.9 mm spline along with mounting hole spacing of 20 mm, 4 mm, and 7.5 mm using M3 hardware.

These measurements will help me design stronger bolt-on brackets in the future instead of having to recreate the servo spline geometry. Using the manufacturer's dimensions will make the connections more accurate and reliable.


**Decisions made**

Finished the CAD design for the shoulder arm.

Made design changes to the base and shoulder components to improve strength and fit.

Decided to use standard 25T servo arms for connecting the robotic arm sections.

Created simple CAD models of the DS3230MG servo and 25T servo arm for the assembly.

Decided to use the manufacturer's mounting dimensions when designing future brackets.


**Next steps**

Continue building the assembly by adding the remaining components.

Continue designing the remaining parts of the robotic arm.


<img width="452" height="578" alt="image" src="https://github.com/user-attachments/assets/1ee5cf7b-3e8b-4716-8505-d559b57e436b" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 7**: July 17, 2026


Time spent: **1.5 hours**


**What I worked on**

Continued working on the CAD design for the robotic arm. Today I spent time making changes to the shoulder base and shoulder arm to improve the overall design. I also continued building the assembly and completed a large portion of it, which helped me better visualize how the components fit together and identify any areas that may still need adjustment.


**What I learned**

Working with the assembly made it easier to evaluate how the different parts interact before manufacturing. Seeing the complete model helped me identify areas where the design could be improved and confirmed that the modified shoulder components fit properly within the overall assembly.

Making adjustments during the CAD stage is much easier than modifying printed parts later, so reviewing the assembly as it develops is an important part of the design process.


**Decisions made**

Made additional design changes to the shoulder base and shoulder arm.

Continued developing the full CAD assembly to verify part placement and overall fit.


**Next steps**

Complete the remaining CAD parts for the robotic arm.

Finish the full assembly and verify that all components fit together correctly.

<img width="662" height="695" alt="image" src="https://github.com/user-attachments/assets/795a2a8e-ebe6-418c-b2ff-691eb02d217c" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 8**: July 18, 2026


Time spent: **1 hour**


**What I worked on**

Continued working on the CAD design and assembly of the robotic arm. Today I decided to replace the remaining MG996R servos with DS3225MG servos after comparing their specifications. I also made several changes to the arm segments to reduce unnecessary material in low-stress areas while maintaining strength where it is most needed. By the end of today's work, the assembly was approximately 80% complete.


**What I learned**

I compared the specifications of the MG996R and DS3225MG servos and found that the DS3225MG provides approximately 25 kg·cm of torque, which is about twice the torque of the MG996R while also costing less. I also learned that the DS3225MG is waterproof and uses metal gears, making it a more durable option for the robotic arm.

After reviewing the manufacturer specifications, I found that the DS3225MG shares similar body dimensions and mounting hole pattern to the MG996R. This means I can switch to the new servos without redesigning the existing brackets or modifying the CAD model.

I also reviewed the arm segments and identified areas where material could be removed without affecting the structural strength of the design. Reducing unnecessary material in low-stress regions should decrease filament usage while maintaining strength around the joints and mounting locations.


**Decisions made**

Selected the DS3225MG servos as the current choice for the remaining joints in place of the MG996R servos.

Revised the arm segment designs to reduce material usage in low-stress areas while maintaining strength around critical mounting points.


**Next steps**

Continue building the remaining CAD assembly.

Complete reset of the Arm.


<img width="553" height="692" alt="image" src="https://github.com/user-attachments/assets/d08b6537-2839-4456-b9ec-4a8b11e3e3be" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 9**: July 19, 2026


Time spent: **4 hours**


**What I worked on**

Finished designing the wrist section of the robotic arm today. I also spent a significant amount of time researching different claw and gripper designs to determine which type would be most suitable for the project. In addition, I went back through several earlier CAD models to add details that I had previously missed, searched for accurate dimension sheets for various components, and worked on troubleshooting a gear meshing issue in the base assembly.


**What I learned**

I researched several different claw and gripper designs, including parallel jaw, two-finger, and three-finger grippers, to compare their advantages and disadvantages for picking up small and lightweight objects. I am still evaluating which design best fits the intended use of the robotic arm.

I spent time searching for manufacturer drawings and dimension sheets for different components and found that measurements often varied between different sellers and sources. This made it more difficult than expected to obtain reliable dimensions and reinforced the importance of verifying measurements before finalizing CAD models.

While reviewing earlier CAD models, I identified several details that I had forgotten to include, such as mounting features and clearances. This highlighted the importance of revisiting completed parts and checking them against the dimensions of the actual hardware before moving on to the next stage of the design.

I also investigated a gear meshing issue in the base assembly. Although the gears used the same module and the theoretical center distance was correct, the gears still interfered with each other at certain rotation angles. I verified that the gear ratio, module, and axis alignment were all correct and determined that the center distance may be slightly too small. I began testing a wider center distance of approximately 31.7–32 mm to determine whether the additional clearance would eliminate the interference while also accounting for backlash and printing tolerances.


**Decisions made**

Completed the CAD design for the wrist section of the robotic arm.

Continued researching claw and gripper designs before selecting a final end-effector design.

Began testing a slightly larger gear center distance of approximately 31.7–32 mm to improve gear meshing and provide additional clearance.


**Next steps**

Continue testing the updated gear center distance to confirm that it resolves the meshing issue.

Finalize the claw and gripper design.

Continue designing the end effector in CAD.

Review the remaining components to ensure that no mounting features, clearances, or dimensions were overlooked before completing the assembly.


<img width="502" height="675" alt="image" src="https://github.com/user-attachments/assets/e0e0fb94-e6ad-4744-bd72-f3fe403ef239" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 10**: July 20, 2026


Time spent: **2 hours 25 minutes**


**What I worked on**

Focused entirely on designing the gripper for the robotic arm. After comparing several end-effector designs in previous sessions, I decided to use a parallel-jaw gripper for the final design.

Most of today's work involved determining the best location for the servo inside the gripper housing and designing the gear mechanism that will transfer the servo's rotation into the opening and closing motion of the jaws. I also continued developing the gripper CAD model while ensuring the components fit together correctly.


**What I learned**

I decided that a parallel jaw gripper is the most suitable design for my project because it provides a simple and reliable way to grip small, lightweight objects.

While designing the gripper, I found that servo placement plays an important role in the overall mechanism. Positioning the servo correctly is necessary to provide enough space for the gears and allow the jaws to move through their full range of motion without interference.

I also designed the gear system that will drive the gripper. This required determining how the servo's rotational motion would be transferred to the jaws while keeping the mechanism compact enough to fit within the gripper housing.

Throughout the design process, I continued verifying dimensions using the servo specifications to accurately position the output shaft and ensure the remaining components aligned correctly.


**Decisions made**

Selected the parallel jaw gripper as the final end-effector design.

Decided to use a gear-driven mechanism to operate the gripper instead of a direct linkage.

Continued refining the servo placement and gear layout within the gripper assembly.


**Next steps**

Finish the remaining CAD work for the gripper.

Verify that the drive gears mesh correctly and make any necessary adjustments.

Test the servo placement within the completed gripper assembly.

Continue finalizing the complete robotic arm assembly.


<img width="777" height="403" alt="image" src="https://github.com/user-attachments/assets/9c631fda-9832-400d-a7ec-c23c53df265e" />
<img width="392" height="431" alt="image" src="https://github.com/user-attachments/assets/03b5c887-9fb7-4648-92c2-211ba3b7dfc2" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 11**: July 21, 2026


Time spent: **4 hours**


**What I worked on**

Finished designing the gripper mechanism for the robotic arm. The final design uses a gear-driven parallelogram linkage that allows the jaws to remain parallel as they open and close. A large portion of today's work was spent troubleshooting issues within the assembly, but by the end of the session I had a fully functioning gripper mechanism.


**What I learned**

While testing the gear system, I learned that correct gear meshing depends not only on the gear dimensions but also on the rotational alignment of the teeth. I found that offsetting the gears by half of a tooth pitch allowed the teeth to mesh correctly instead of overlapping.

I also discovered that an incorrect center distance can appear to be a gear alignment problem. After checking the gear dimensions, I found that my center distance was slightly smaller than the calculated value. Correcting it to 31.5 mm resolved the remaining interference between the gears.

While assembling the four-bar linkage, I learned that adding unnecessary constraints can cause the assembly to become over-constrained. Once the linkage was built using the correct pivot locations and dimensions, the mechanism maintained its motion without requiring an additional parallel constraint.


**Decisions made**

Completed the final gripper mechanism using a gear-driven parallelogram linkage.

Removed the unnecessary parallel constraint from the assembly.


**Next steps**

Address the remaining issues.

Finish the complete robotic arm assembly.

Continue testing the gripper to verify its full range of motion.


https://github.com/user-attachments/assets/6f530a01-1f68-40d2-a437-52708d4fa79e

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 12**: July 23, 2026


Time spent: **2 hours**


**What I worked on**

Finished troubleshooting the remaining issues in the robotic arm and completed the full CAD assembly. After making the final adjustments, I verified that the entire assembly functions correctly and that all of the major components fit together as intended.


**What I learned**

Completing the full assembly allowed me to evaluate the robotic arm as a system rather than testing each section individually. This made it easier to identify how changes in one component affected the rest of the design and confirmed that the base, shoulder, elbow, wrist, and gripper all operate together as expected.

I also learned that completing the full assembly is an important step before manufacturing because it helps reveal any remaining alignment or interference issues that may not be obvious when parts are designed separately.


**Decisions made**

Completed and verified the full robotic arm assembly.

Confirmed that the core mechanical design no longer requires any major redesigns.

Shifted the project's focus from design work to final verification and refinement.


**Next steps**

Perform a final review of every part by comparing dimensions with the actual hardware specifications.

Make any final adjustments that are identified during the review.

Complete the bill of materials and calculate the final estimated project cost.


<img width="1252" height="745" alt="image" src="https://github.com/user-attachments/assets/f61de71a-2e87-4aa4-85aa-c128c3cc569e" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
