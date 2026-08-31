# Skills Canada Mobile Robotics 2026

## Overview

Designed, built, and programmed two tele-operated robots and one autonomous robot for the 2026 Skills Canada Mobile Robotics Competition, ultimately earning a Provincial Gold Medal and representing British Columbia at the Skills Canada National Competition.

**[Watch one of our matches at the Skills Canada National Competition](https://www.youtube.com/watch?v=wze2jL2ozuA)**

While there are additional code and CAD files related to this project, this repository only contains files that I personally worked on.

## Project Highlights

- Provincial Gold Medalist, Skills Canada BC 2026
- Represented British Columbia at the Skills Canada National Competition
- Co-led and coordinated a team of 10 students
- Designed and programmed three competition robots
- Developed autonomous systems using inertial sensors, PID control, and data logging
- Created autonomous tuning software with SD card data storage
- Contributed over 250 hours during an eight-month design period

## Game Description

The 2026 Skills Canada Mobile Robotics challenge simulated a burning factory. The robots were tasked with:

- Clearing debris (pool noodles, 2×2s, and wires) from hallways
- Gaining access to rooms by removing fallen beams
- Removing damaged fuses, circuit boards, and transformers from an Environmental Control Unit (ECU)
- Replacing damaged components with functioning ones
- Autonomously delivering supplies to safe zones for trapped workers

For a complete description of the challenge, see [Mobile Robotics 2026 Game Description](Mobile%20Robotics%202026%20Game%20Description.pdf).

## My Role

I served as a team leader, delegating tasks to nine junior members and collaborating with my co-lead on robot design and game strategy.

While design was my primary focus for much of the project, I also programmed the autonomous robot and one of the tele-operated robots, as well as 3D-modeled several custom components. Additionally, I operated one of the tele-operated robots at the regional, provincial, and national levels.

The design, manufacturing, programming, and testing process spanned approximately eight months and required over 250 hours of work on my part.

## Technologies Used

### Hardware

- VEX V5 Robotics Equipment and Sensors
- Custom 3D-Printed Components (PLA and PETG)

### Software

- C++
- VEXcode V5
- Autodesk Inventor
- Autodesk Fusion 360
- PID Control
- CSV Data Logging

## News Coverage

As part of our fundraising efforts for Nationals, our team was featured in local news coverage and a school district publication.

- [School District 68: Dover Bay students will put robotics skills to the test on the national stage](https://www.sd68.bc.ca/dover-bay-students-will-put-robotics-skills-to-the-test-on-the-national-stage/)
- [NanaimoNewsNOW: Dover Bay robots charging up for nationals](https://nanaimonewsnow.com/2026/05/04/dover-bay-robots-charging-up-for-nationals/)

---

# CAD Components

## Circuit Board Holder

![Circuit Board Holder](Photos/Prototype%20mech%20for%20inserting%20circuit%20boards.jpg)

The two pieces shown above are the primary components of a mechanism used to remove broken circuit boards from the ECU. Once removed, the boards are retained by the robot until they can be deposited in the debris zone at the end of the match.

## Circuit Board Inserter

![Circuit Board Inserter](CAD%20Designs/Circuit%20Holder/Circuit%20Holder%20Assembly%20-%20Screenshot.jpg)

The two pieces shown above are the primary components of a mechanism used to pick up replacement circuit boards from their starting position and insert them into the ECU.

## BeamWheel2

This component was designed to spin at high speed and remove fallen beams blocking access to rooms within the game field.

## Fuse Holder

![Fuse Holder](Photos/Early%20Prototype.jpg)

This component was part of an early robot prototype. The original concept involved using a claw to pick up replacement fuses and insert them one at a time into the holder.

However, the design was ultimately deemed too slow and was abandoned. A photo of the final mechanism can be found in [here](Photos/Final%20mech%20for%20inserting%20fuses.jpg). The final version was not designed by me.

---

# Code

## ECU Robot Driver Control v4.5

This is the final version of the driver-control code for the robot responsible for inserting replacement components into the ECU.

Because the controller did not have enough buttons for every required function, I created a system with three button modes. Drivers could press two buttons simultaneously to switch modes, changing button functions and aligning drive orientation with the mechanism currently being used.

## Macro Autonomous Code

The goal of this system was to allow a driver to complete the autonomous challenge before competition while recording movement data, then replay that data later without driver input.

Although the concept showed promise, it was ultimately abandoned because it introduced too many sources of error, particularly driver inconsistency and sensor inaccuracies.

### Recording

Recorded drivetrain and mechanism data using motor encoders and inertial sensors, storing motion profiles as CSV files on an SD card. The system automatically identified waypoints and optional pauses for later replay.

### Replay

This function reads recorded data from the SD card and separates motion into sensitive and non-sensitive segments.

When only the drivetrain was moving, the robot could travel as quickly and accurately as possible using PID control. However, when mechanisms such as intakes or conveyors were operating simultaneously, the replay system matched the recorded velocities to preserve timing and coordination.

Additionally, if a pause was not marked as necessary during recording, the replay system automatically removed it and proceeded directly to the next segment.

## Final Autonomous Code

While somewhat anti-climactic, I found that simple commands such as "drive x inches" or "turn y degrees" were significantly more reliable than the Macro Autonomous system.

To improve turn accuracy, we used two inertial sensors and averaged their readings. These sensors were used primarily for precise heading control during autonomous operation.

![Autonomous Robot](Photos/Auton%20Robot.jpeg)

### Tuning Code

The data-saving functionality of this system was inspired by the earlier Macro Autonomous project.

One of the biggest challenges with traditional autonomous programming was the amount of time required to repeatedly adjust values, recompile code, and download it to the robot. This system solved that problem by allowing autonomous parameters to be adjusted directly through a simple controller-based user interface.

Drive distances could be modified using controller buttons and saved to the SD card as a CSV file. The system also allowed users to select the fan position (one of three possible starting locations determined before each match) through a simple interface on the robot brain.

### Run Code

This code is similar to the tuning system but does not allow user interaction after autonomous mode has started and the fan position has been selected.

This restriction was necessary to comply with competition rules during official autonomous runs.
