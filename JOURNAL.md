# 3/15/26, Day 0:The thesis 

I was in the midst of a debate regarding a certain sub-one-minute record being set (or forged, is the better way to put it.) The debate eventually shifted to analyzing the technical specifications of machines that legitimately set these records. I naturally became intrigued by this discussion, analyzing machines like Roetz’s Minuteman, Kevin’s Kevender, and Vlogger’s WildSau Reborn. These are all impressive works of engineering, with insane amounts of tuning and new technologies that haven’t been applied commercially, let alone be tested on standard 3d printers.

 Despite their mind-boggling technologies, I found myself easily understanding the science behind these machines, and began subconsciously planning optimizations and ideas for these machines. With a pile of 3dp hardware sitting around, these ideas, and infill V2, I decided, that I wanted to join the race with a make a machine of my own, with completely experimental technologies, and ideas to set the world record. 

# 3/16/26, Day 1: Research & Planning 

Machines built to set world records are not cheap. I decided to use Kevin's kevender as a basis to compare theoretical specifications of my machine to, as despite it being a 2 minute benchy, it still was far much more capable and held the world record for a substantial amount of time.   
I decided to fit my budget requirements, I would use 4x LDO 2804AC motors (short shaft), and my BTT manta m8p, e3d supervolcano, and to give it that “Thing-O-Matic” reprap vibe with the utilization of a completely printed structure. Thanks to a polymaker sponsorship of mine, the machine can be printed completely out of PET-CF17, an incredibly stiff, yet easy to print carbon-reinforced filament with incredible thermal resistance. The parts would need to be printable on my Prusa Core One. I have spare belts, pulleys, and an assortment of bearings along with a small power supply to power most of the auxiliaries on the machine. I also have a CPAP blower and an assortment of fans making the bulkhead of components purchasable with the upgraded 350$ grant.   
Looking at the leaderboards, I noticed that both the Minuteman and Kevender utilize bedslinging motion, as the theoretical weight of the bed is far lesser than that of a tool/gantry slinger.   
I decided, as I do want to keep some practicality in the machine, I would utilize CoreXY as a bedslinger, meaning that while it does use Corexy, the bed moves in the XY directions.  
I also decided that since the toolhead was not required to be lightweight, I would utilize a supervolcano with an upgraded heater, heatshield, CPAP blower, and multiple melt-zone extended geometry assistants. With all of that basic stuff in mind, I put these following points on the drawing board to think about while designing the printer:

* 4WD Liveshafted 56V bedslinger gantry

* Dual gear/dual motor boombox-inspired extruder for maximum torque and grip

* 72MM Meltzone

* Either no heater, or direct carbon heating by running current through the carbon fiber bed sheet as a resistor 

* CPAP/high power cooling, possibly experiment with technologies/ideas to overcome the low cooling capacity of air

* 100% printed structure for frame and enclosure, printable of prusa core one

* Bed fits a benchy

# 3/20/26, Day 2: Gantry 

### Beltpaths? 

Like most corexy machines, there are two belts that ride one another. High performance machines need more tension, which can increase racking and bearing wear. Having this in mind, I need a way that can handle extreme belt tension without damaging the idlers, motor, or motor shaft. This generates a lot of **shear stress**, which risks bending motor shafts, or the load damages bearings, especially smaller ones. This means two things, I need to counteract this shear stress, and not damage the bearings. This means, I will have to design a system that uses **Double Shear**.  

<img width="512" height="147" alt="image" src="https://github.com/user-attachments/assets/45d20ca0-6d9f-426b-81fc-c1f7f235b1ef" />

Double shear helps to equalize shear stress on a system, greatly reducing the strain on the belt pulleys and idlers. This also meant that because of this high force, I would need large bearings. The small bearings seen in toothed idlers simply could not handle belt forces under extreme tension (and prematurely wear out in normal tension anyway), So the solution is to utilize larger bearings. Since the toothed idler’s size needs to be maintained, this isn’t easy. The solution? Use a mechanism called a liveshaft.

<img width="305" height="512" alt="image" src="https://github.com/user-attachments/assets/1bf48b15-91e6-470b-b157-d37949471595" />

These allow the idler to remain a solid chunk of metal, and the shaft simply re-distributes the load to the 2 large bearings instead. 

Due to the size constrains of the printer, i also need to make the gantry relatively compact. In order to achieve high speeds reducing weight, belt length, and friction are instrumental to gaining speed. Similar to what the snapmaker U1 and bambulab x1c/p1 series, i can use carbon fiber rods for the X axis, using polymer bearings. While some users have reported potential residue buildup on the rods, it’s simply the wear of the bearings as they create a coating on the rods in order to reduce friction. Even with thousands of hours, these bearings have shown minimal wear and are easy and cheap to replace. Because i already have a pair and they are incredibly low friction and easy to integrate into this machine, i can go forward with MGN12H rails for the y axis, and connect them to the frame. Because i need to use double shear with short-shafted motors, i have to opt for utilize 6mm belts instead as the shaft isnt long enough to support larger pulleys. This means belt stretch may result in a loss of effective gantry stiffness, indicated by a loss in scaling on the resonance generation graphs, which i will have to look out for. Thankfully, with an incredibly stiff and robust gantry, and minimized belt lengths, this can be mitigated with higher belt tensions which i will need to tune. Using all this information i created the gantry.  

<img width="512" height="436" alt="image" src="https://github.com/user-attachments/assets/a4f6c39d-2214-4590-829e-fdb95cde2ecc" />

# 3/22/26, Day 3: The body

The body panels are relatively simple. Similar to the makerbot thing-o-matic and many reprap printers, i can use interlocking panels that are fastened. This means thing-o-mega can be created out of a variety of materials, from laser-cut plywood, acrylic, to waterjet metals and printed sheets. To reduce fabrication costs I can utilize polymaker’s pet-cf17, an incredibly stiff and heat resistant plastic which will aid in effective printer stiffness to maintain quality at higher acceleration.  
I then created a series of printable panels that i can print on my prusa core one. I will likely need to clearcoat the corners as loose chopped fibers can irritate the skin.  
I can also utilize a 3d pen to effectively “weld” the exoskeleton together.  

<img width="479" height="512" alt="image" src="https://github.com/user-attachments/assets/7238b3d8-d11f-4743-8f71-3a32ffb664a4" />

# 3/23/26, Day 4: The Z axis 

Because the Z axis is responsible for all of the toolhead motion, there’s a lot of freedom to be had. Technically, i wouldn’t even need a probing system as it can be done manually, however a method to home Z reliably would help with overall reliability. While hotend stiffness isn’t necessary for performance, a long meltzone that i would likely need would be vulnerable to damage with gantry crashes at over 4000mm/s.  
I then looked at some more unique systems and developed my own tap-based probing system. Similar to voron tap, the nozzle is allowed a certain amount of undetermined movement in the Z axis. It then moved to a certain trigger threshold to detect offsets and probe activation. These systems however suffer from toolhead stiffness and weight problems, however are also less affected by crashes as the nozzle is allowed to move up and down. This system is similar to voron tap, however the entire gantry is allowed to move up and down on z, however a known minimum position is always known. Should a crash occur, the gantry will simply maintain it’s position or any forces on the hotend dissipate into Z movement.  

<img width="512" height="385" alt="image" src="https://github.com/user-attachments/assets/04b7474c-2f30-4d11-b9f5-66a3d52f5e9c" />

 
The Gantry part with the extrusions simply rides atop the “blocks”, and a microswitch is used to detect if a gap between the two exist.   

<img width="512" height="322" alt="image" src="https://github.com/user-attachments/assets/490102b7-2b2e-4f66-9208-4192e0bc83a8" />


A simple dual rod and leadscrew motor allows the gantry sections to move up and down with ease. 

<img width="512" height="308" alt="image" src="https://github.com/user-attachments/assets/1b2ab428-b397-4c9a-b41a-41e41173a373" />

# 3/24/26, Day 5: Toolhead, Part one 

## Overview

The toolhead is an interesting part of this machine. Much more design freedom is granted thanks to no requirement of weight savings or size, allowing me to utilize the entire gantry’s size to build the toolhead. This means i can develop a very large hotend without performance losses, along with a very large extruder and cooling system. As i already have a spare ws7040, i can use that to pump air for the toolhead.

## Hotend

The current limitations for a large percentage of the leaderboard positions are limited by extrusion. I decided i can use my spare supervolcano hotend, granting me 50mm of meltzone length. Because i plan to push things further, an over provisioned meltzone allows me to achieve the same flowrates with lower temperatures, as cooling is the current world record holder’s bottleneck. I switched the heater cartridge with a 120W heater to support these higher flowrates, along with the cooling system’s added losses. I added a MZE (meltzone extender) and utilized the coldend of the dragon HF hotend, which has a heatbreak that acts like an MZE. This grants me a total meltzone length of a whopping 72mm.

<img width="487" height="512" alt="image" src="https://github.com/user-attachments/assets/ea732457-59ee-409d-addc-6b5e7027bec1" />

#  3/25/26, Day 6: Toolhead, Part Two 

## Extruder

While the hotend can now support extremely high flowrates, at higher filament speeds many extruders experience a loss in total torque as they need to be lightweight enough to allow the toolhead to move. Many circumvent this with the use of a Bowden extruder, however quality losses occur with pressure advance numbers increasing. One of the best extruders suited for this application is the boombox, a bmg-based dual motor closed source extruder capable of incredible strength and speeds. I decided to take inspiration from such an extruder, and developed the VHS-Extruder, (Very high strength, also resembles a vhs tape.). Similar to the boombox, it uses two stepper motors, attached to BMG hobs and bearing idlers to press down on the filament. Rather than adopt a common dual gear design, the bearings are less prone to producing a “skin” effect and are thinner than bearing bmg hobs, allowing for efficient packaging of the extruder, and the dual motors allowing for adequate grip. 

<img width="446" height="512" alt="image" src="https://github.com/user-attachments/assets/bfbeea7a-ca30-4380-a17d-b0ede37b549b" />

The two inverted arms push against the washer, which is attached to an M5 bolt and a spring. Unlike the boombox, it is open source and not behind a 10 dollar paywall, however most of my credits, inspiration, and respect does go to the creator of the boombox.   


Package it all up, and add a small cooling shroud, and the extrusion setup is complete. 

<img width="512" height="385" alt="image" src="https://github.com/user-attachments/assets/2b2c528f-9a27-4555-a42e-31d8ff19cc81" />

## Ducts

This one is one that cannot be forgotten. The current bottleneck, reported by the current world record holder roetz, is stated to be cooling. He utilizes a Bike needle and compressed air setup, Taking advantage of high velocities and marginal gains due to adiabatic cooling thanks to pressure losses. If i plan to shoot to compete with such a machine, i need to be efficient with my own cooling system too. Using a cpap blower, I technically have much more volume than roetz, however my air temperatures, velocity, and pressure are much lower. With this, I decided to create a duct with heavy forward bias. 

<img width="429" height="512" alt="image" src="https://github.com/user-attachments/assets/05760265-cd59-4140-afe4-4ca65168f107" />

The heavy forward bias allows for a greater amount of total air flow across the print, and allows for effective cooling of all zones. The reduction at the outlets is rather large, especially given the ws7040 but I do plan to experiment with using different blowers (such as a shop vac), or some other ideas for cooling. In order to smoothen the bend as the cpap blower will be placed in a remote location, a smooth angled transition was added. 

<img width="511" height="512" alt="image" src="https://github.com/user-attachments/assets/39d2b84f-8c1d-402f-89ad-4cfe3f6bad60" />

Any losses caused by this bend is rather marginal, however some bias may be generated.   

<img width="512" height="202" alt="image" src="https://github.com/user-attachments/assets/8b7d853f-3c1d-4f6f-be09-c67e71facfac" />

The ducts also feature vanes to help smoothen and laminarize the airflow upon exit, as turbulence outside the duct can ruin any venturi effect gains. 

# 3/26/26, Day 7: Cooling system 

As I have stated before, Cooling is the main bottleneck in nearly all speedboat race machines. The conductivity of normal air is rather poor, so large amounts at high velocities and low temperatures are used to help cool prints at such speeds. I noticed roetz had experimented with dry ice to generate ambient air temperatures far below zero, along with a prusa modified to print underwater. It had great performance, however it was expensive (already cannot afford that) and there were issues with layer adhesion. I did notice that ice crystals formed, and thought, why stick with air? I decided perhaps utilizing a water-atomized spray might prove useful as water is 25X more thermally conductive, and has a volumetric heat capacity 4000 times that of air. If I cannot move air faster than other systems, I figured I might as well move a different material altogether instead. I then created a simple Atomization unit, taking in dry air (from a cpap blower or some other air supply), and running it through a simple box of 12 ultrasonic atomizers.

<img width="381" height="512" alt="image" src="https://github.com/user-attachments/assets/f176c2c1-2c11-4f4a-930e-6c6390259e36" /> 

<img width="512" height="271" alt="image" src="https://github.com/user-attachments/assets/d46ebaf1-2482-4679-9141-61bca6f9774b" />

 I may need to experiment with baffles on the lid to “Stir” the air around. The outlet is placed at the top to avoid large amounts of water splatter and heavy droplets from going into the duct. One potential challenge with this system is that high pressure changes and turbulence may create “Slobber” in the ducts, where the atomized water molecules may bond in the duct, turning it from a nice clean mist, into a messy stream of water. Plastic also does not like to bond to water, so layer adhesion issues could potentially be caused by water accumulating on the prints. Luckily I will be using 3 driver boards, each controlling 4 modules. By using the 5v fan control pins on the manta m8p, I can control the atomizers in increments of 3, allowing me to adjust the water content of the air, possibly mid print to control the cooling system precisely. I can also experiment with different water temperatures, possibly using boiling water to avoid the “Slobber” issue and overcooling of the print, or ice water to increase the efficiency of the cooling system. 

# 3/27/26, Day 8: Electronics 

This part is pretty simple but we do need to package the electronics, and add any extra systems to aid in cooling the motors.

<img width="512" height="357" alt="image" src="https://github.com/user-attachments/assets/8d416c30-1e2f-4b89-adb7-2ba5101988ca" />

The board is simply placed at the bottom, with heatsinks mounted to cool the gantry motors. The natural convection should be adequate to cool the printer, however it’s pretty easy to add cooling fans down there if needed. 

# 3/28/26, Day 9: Conclusion 

With that, the easy parts are completed. Cadding, and designing are important steps of the process, but the journey doesnt end here. Racing machines take countless hours of tuning and experimentation to perfect achieving great speeds, However I’m excited to see what this thing can do.   

<img width="512" height="406" alt="image" src="https://github.com/user-attachments/assets/ba955b2e-fdd6-48ca-9945-df772e3c1eda" />
