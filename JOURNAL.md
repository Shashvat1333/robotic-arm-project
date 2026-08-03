Robotic Arm Project Journal
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 1**: July 11, 2026

Time spent: **2 hours**

Started planning the robotic arm today, mostly research before touching CAD. Compared 3, 4, 5, and 6 DOF designs, and I'm currently leaning toward 6 DOF since it gives more flexibility, even though it adds complexity. Looked into open-loop vs closed-loop servos and decided open-loop PWM should be fine since my payload is under 500g. Also learned torque needs go up the closer a joint is to the base, so I'm planning stronger servos like the MG996R for the base and shoulder and weaker ones like the MG90S for the wrist and gripper. Picked the ESP32 over Arduino mainly because of the built-in WiFi.
Next: build a BOM, calculate real torque numbers, start early CAD sketches.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 2**: July 12, 2026

Time spent: **2.5 hours**

Ran actual torque numbers today. With a 42cm arm and 100g payload, the shoulder needs about 15.4 kg cm of torque, which is more than a standard MG996R can handle comfortably. Switched the base and shoulder servos to the DS3230MG since it gives a lot more headroom. Updated my planned lineup to two DS3230MG for base and shoulder, two MG996R for elbow and wrist pitch, and two MG90S for wrist roll and gripper. Also bumped my power supply up to 5V 10A after realizing worst-case current draw could hit 9 to 13A.
Next: finish the BOM, design brackets for the heat set inserts, check clearances before printing anything.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 3**: July 13, 2026

Time spent: **4 hours 30 minutes**

Started actual CAD today, focused mostly on the base gear system. I wanted full 360 rotation out of a 270-degree servo instead of adding a slip ring, and worked out that a 3 to 4 step up gear ratio would do it. My first gear sizes were too small, and the teeth interfered with each other, so I bumped them up to 18 and 24 teeth using the same ratio, and that fixed it. Learned a lot about using Onshape's gear tools and Revolute Mates to get the assembly moving correctly. Also planning to pad the center distance slightly to account for printing tolerances.
Next: finish the base gear housing, print and test the gear pair, then move on to the shoulder.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 4**: July 14, 2026

Time spent: **3 hours**

Spent today researching print tolerances to get the base and shoulder parts ready for actual printing. CAD for the shoulder and base parts is now roughly 75% complete. Looked into clearance rules for press fit and moving parts, and figured out proper hole sizing for the M3 heat set inserts. Also researched how to install the inserts properly with a soldering iron without making a mess around them. Settled on doing dimensional adjustments directly in CAD instead of relying on the slicer, and picked print settings for the smaller detailed parts.
Next: finish the base and shoulder parts completely.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 5**: July 15, 2026

Time spent: **2 hours**

Finished the base and shoulder components and started building the full assembly to see how everything actually fits together. Caught a small mistake where my insert hole size was slightly off from the manufacturer spec and fixed it. Seeing everything together made it a lot easier to spot interference issues that weren't obvious when parts were designed separately. Added some fillets and reinforced a few areas that looked like they'd crack under load.
Next: keep building the assembly, check remaining parts for weak spots, finish the rest of the CAD.

<img width="532" height="653" alt="image" src="https://github.com/user-attachments/assets/c359f7c1-f972-4ee5-9dc3-7ed324049b32" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 6**: July 16, 2026

Time spent: **5 hours**

Finished the shoulder arm and made some strength improvements to the base and shoulder parts. Decided to use standard 25T servo arms instead of designing custom connectors, so I made quick models of the DS3230MG and a 25T arm to check the fit in the assembly. Found the actual manufacturer mounting dimensions for the servo, which should make future brackets a lot more accurate.
Next: keep adding parts to the assembly and keep designing the rest of the arm.

<img width="452" height="578" alt="image" src="https://github.com/user-attachments/assets/1ee5cf7b-3e8b-4716-8505-d559b57e436b" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 7**: July 17, 2026

Time spent: **1.5 hours**

Made more changes to the shoulder base and arm and kept building out the assembly. Nothing too dramatic today, mostly just confirming everything still fits properly once I could see it all together. Reminded me again that catching problems in CAD is a lot easier than catching them after printing.
Next: finish the remaining CAD parts and confirm the full assembly fits.

<img width="662" height="695" alt="image" src="https://github.com/user-attachments/assets/795a2a8e-ebe6-418c-b2ff-691eb02d217c" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 8**: July 18, 2026

Time spent: **1 hour**

Swapped the remaining MG996R servos for the DS3225MG since it gives roughly double the torque for less money and is waterproof with metal gears. Turns out the mounting pattern is basically the same, so I didn't need to redesign any brackets. Also trimmed some unnecessary material out of low-stress arm segments to save filament. Assembly is around 80% done now.
Next: keep building out the rest of the assembly and clean up the arm CAD.

<img width="553" height="692" alt="image" src="https://github.com/user-attachments/assets/d08b6537-2839-4456-b9ec-4a8b11e3e3be" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 9**: July 19, 2026

Time spent: **4 hours**

Finished the wrist section today and spent a good amount of time comparing gripper designs, still deciding between a few options. Found out dimension sheets for the same part can vary a lot between sellers, so I can't just trust one source. Went back through some older CAD parts and found details I'd missed earlier. Also ran into a weird gear meshing issue in the base where everything checked out on paper but the gears still interfered at certain angles, so I'm testing a slightly wider center distance to fix it.
Next: confirm the wider center distance works, finalize the gripper design, keep reviewing older parts.


<img width="502" height="675" alt="image" src="https://github.com/user-attachments/assets/e0e0fb94-e6ad-4744-bd72-f3fe403ef239" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

Day 10: July 20, 2026
Time spent: 2 hours 25 minutes
Locked in the parallel jaw gripper design and spent most of the day figuring out where to put the servo inside the housing and designing the gear mechanism that turns the servo rotation into the jaw movement. Servo placement mattered a lot more than I expected, get it wrong and there's no room for the gears or the jaws can't move properly.
Next: finish the gripper CAD, check that the drive gears mesh correctly, test the servo placement. 

<img width="777" height="403" alt="image" src="https://github.com/user-attachments/assets/9c631fda-9832-400d-a7ec-c23c53df265e" />
<img width="392" height="431" alt="image" src="https://github.com/user-attachments/assets/03b5c887-9fb7-4648-92c2-211ba3b7dfc2" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 11**: July 21, 2026

Time spent: **4 hours**

Finished the gripper mechanism today using a gear-driven parallelogram linkage so the jaws stay parallel while opening and closing. Spent most of the time fighting the gear problems from earlier and learned that correct meshing depends on rotational alignment too, not just size. Fixed it by offsetting the gears by half a tooth pitch. Also found what looked like an alignment problem was actually just a center distance that was slightly too small. One more issue came from over-constraining the linkage, removing an extra constraint let it move freely on its own.
Next: fix remaining issues, finish the full arm assembly, keep testing the gripper's range of motion.

https://github.com/user-attachments/assets/6f530a01-1f68-40d2-a437-52708d4fa79e

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 12**: July 22, 2026

Time spent: **2 hours**

Finished troubleshooting and completed the full CAD assembly today, base, shoulder, elbow, wrist, and gripper all working together. Testing everything as one system made it much easier to see how changes in one part affected the rest. No major redesigns needed at this point, so I'm shifting into verification mode.
Next: do a final review of every part against real hardware specs and finish the BOM.

<img width="1252" height="745" alt="image" src="https://github.com/user-attachments/assets/f61de71a-2e87-4aa4-85aa-c128c3cc569e" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 13**: July 23, 2026

Time spent: **3 hours**

Reviewed every CAD part looking for mistakes and fixed what I found. Worked out wire routing, leaving extra slack at each joint so the servos can move freely without pinching anything. Tried exporting the assembly to PyBullet and ran into a wall, it detected zero degrees of freedom, meaning none of my mates were recognized as actual joints. Also found some parts were missing material properties.
Next: fix the assembly mates, assign material properties, and try exporting again.

<img width="370" height="750" alt="image" src="https://github.com/user-attachments/assets/df353599-1760-4c87-a56d-3c538e7c4aa8" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 14**: July 24, 2026

Time spent: **2.5 hours**

Wanted to make an animation of the arm moving so I could see how the joints work together before building the real thing, thought it would be quick but it wasn't. Tried the PyBullet route again and hit the same issues as before. Ended up using Onshape's Gear Relation feature instead to link the joints together so one driving joint animates the whole arm at once. Good enough to demo the motion for now.
Next: keep improving the joint definitions, finish the remaining CAD, start pricing out the parts list.

<img width="1096" height="718" alt="Main Arm" src="https://github.com/user-attachments/assets/517648e7-f72f-484d-bfb2-2633fb299878" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 15**: July 26, 2026

Time spent: **2 hours 30 minutes**

Finalized the BOM today and went through every component to make sure nothing was missing. Swapped some Amazon.com parts for Amazon.ca ones to save on shipping and import costs. Added a fuse holder to protect the ESP32 that I'd missed before. Learned some cheap MG servos only have metal gears on part of the gearbox, the rest is plastic, which is fine for this build but good to know for later. Total estimated cost came out to around $257.10 CAD.
Next: make final CAD tweaks, apply for the grant, start the physical build once parts arrive.

<img width="963" height="565" alt="image" src="https://github.com/user-attachments/assets/1f65228f-46b7-4440-ae68-95d81e294ded" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Day 16**: July 27, 2026

Time spent: **1 hour 47 min**

Added real M3 screw and heat set insert models into the assembly instead of just leaving the mounting holes empty. Makes the whole thing look and feel more real, and it's genuinely useful, putting the hardware models in exposed a few clearance and fit issues I hadn't noticed before. Fixed those before printing.
Next: apply for the Stardance grant once the form's back up, order parts once budget's confirmed, start the physical build.


<img width="553" height="266" alt="image" src="https://github.com/user-attachments/assets/9301283e-7855-48a1-abfd-7b75c069d0c7" />

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
