[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/kzkUPShx)
# a14g-final-submission

    * Team Number: 4
    * Team Name: Ad Astra
    * Team Members: Miles Osborne & Oryza Tarigan
    * Github Repository URL: https://github.com/ese5160/a14g-final-submission-t04-ad-astra.git
    * Description of test hardware: Windows 10 Laptop, Atmel SAMD21 Microcontroller Unit + ATWINC1500B Wifi Module, Ad Astra - Pocket Star 1 (PS1) PCBA, GPS Sensor (ST Microelectronics Teseo LIV3R GPS/GNSS), GNSS / GPS Development Tools GNSS expansion board based on Teseo-LIV3F module for STM32 Nucleo (STMicroelectronics 511-X-NUCLEO-GNSS1A1), Bipolar Stepper Motor Hybrid Frame Size 11 200.0 Step 670 mA 4.56VDC (Pololu 1206)

## 1. Video Presentation

### Introduction
This video presentation explained the project in general. The video can be accessed in the following URL.
<br><https://drive.google.com/file/d/1v15rwJ6hfAnth5Jb4qp1i7n2fG27neqQ/view?usp=sharing>

### Functionality Demo
This video presented the device functionality demo in detail. The video can be accessed in the following URL.
<br><https://drive.google.com/file/d/1qdvwb2m9TCKmDlxzcKZrhUnrN8dQ3L_Q/view?usp=sharing>

### OTAFU Demo
This video presented the OTAFU demo in detail. The video can be accessed in the following URL.
<br><https://drive.google.com/file/d/1u-ZVgk9OZaX1GkLECISm4cKjSkv0HLOG/view?usp=sharing>

## 2. Project Summary

### Device Description
The device is called **`Pocket Star 1 (PS1)`** which is a “smart” star tracker. A star tracker is a tool used in astrophotography to help align the camera’s lens with the Earth’s rotation and follow the target’s path.

The device capable of doing configuration to adjust the rate and for how long it tracks the object and an auto-polar alignment feature as an essential feature.

Additional features are also centered around user input and feedback. Through a user interface such as Node-Red, we shall allow users to select what star or astronomical object they would like to view before the tracking starts and display statistics such as time remaining for the current tracking session. Lastly, for the wireless connectivity aspect of the system, we shall support over-the-air firmware updates in the case that we have to make changes in the field or outside of development.

### Inspiration
Traditionally, every star tracker requires polar alignment before it can be used each time. This is usually a manual process that can take a few minutes to get right. Similarly, many star trackers allow for some form of configuration to adjust the rate and for how long it tracks the object. This device intends to replicate some of these functions (on a smaller scale) but also automate some of the manual aspects involved with the process. To the best of our knowledge, this has not been a feature incorporated on any star tracker currently available for purchase.

### Device Functionality
The device functionality can be obeserved in detail in the following detailed system block diagram.

<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/905ddb12-668e-4f96-a08b-f5ec5d82b2a6" alt="Detailed System Block Diagram">

What the device do:
1. User puts the device facing north somewhere in northern hemisphere.
2. The device detects the current location using GPS sensor and the GPS data is sent to the dasboard for user to view.
3. Based on user input from the dasboard, the device can start polar alignment by pressing `Update Polar Alignment` button in the dashboard.
4. Once the message received from the server (dashboard) the device now move the stepper motor 2 on y-axis to align to the north pole.
5. After the alignment process finished, the dashboard will indicate it to the user. Now, user can decide: (1) Which object to track and (2) how long will the object be tracked. Once user push the `Start Tracking Object` button, the tracking sequence will be commenced.
6. When the device received the message from the server, the device start tracking the object by moving the stepper motor 1 on x-axis for the amount of time input by the user.
7. Once tracking completed, the stepper motor will move back to its initial position and the dashboard will indicate that the process is done.
8. All the process can be repeated from 1 to 6 or if the user want to track other object, just repeat step 4 to 6.

### Challenges
1. Memory management using FreeRTOS causing undefined and unexpected behavior
   - Back tracking with commit history and experimenting with the FreeRTOS config file. Some passing knowledge of the max heap size and the behavior that caused helped in diagnosing the issue and eventually reaching the solution. 
2. Proper RF routing for the GPS/GNSS module on the PCB
   - We were not able to resolve this issue so we decided to substitue the GNSS module with its breakout board. 
3. Diagonising errors with the boost regulator
   - Debugging sessions eventually pointed to the resistors being the cause of the irregular voltage
4. Multiple pads and traces were ripped when assembling our PCB
   - We still are not entirely certain what caused this but it made validating our power management systems more difficult than it otherwise would have been.
5. General ambition of the project. Too many moving parts for two members in a single semester. 
   - It took us a little longer to get our project in a working state but reducing the scope slightly likely would have been a better approach. 

### Prototype Learnings
#### Lessons Learned:
- Think ahead of time about mounting solutions for the whole system
- Learned better PCB design techniques particularly regarding power management and planning
- Expose I/O lines and test points.
  - This saved us and made it possible to attach a breakout board of our GNSS module while the onboard module was unresponsive

#### Changes for next time: 
- I/O exposed on the enclosure of the box
  - LEDs
  - Buttons
  - USB port

- Stronger stepper motors
  - We severly underestimated the torque of the motors we selected so there was concern on if it would be able to actually hold a small mirrorless camera  
  
- Integrate gearing system to get a more precise rotation in line with orbital rotation speeds. Microstepping alone likely wouldn't get the resolution we need.

### Next Steps
- Integrate an IMU to get orientation data to make it fully self-aligning
- Further investigate the onboard GPS and redo the RF routing
  - Might require an increase in PCB size.

### Takeaways from ESE5160
- It was interesting to go from start to finish of the design process albeit with a few steps out of order. The biggest takeaways came from the PCB design/manufacturing section since that was the content most unfamility to us. 

### Project Links
Some project links for review are listed below.

 | Description | URL |
 | ----------- | --- |
 | Node-RED Dashboard | <http://20.81.250.63:1880/ui> |
 | Node-RED Backend | <http://20.81.250.63:1880> |
 | Final Embedded C Firmware Codebases (A12G Code Repository) | <https://github.com/ese5160/a12g-firmware-drivers-t04-ad-astra.git> |
 | Node-RED Dashboard Code (A12G Code Repository) | <https://github.com/ese5160/a12g-firmware-drivers-t04-ad-astra.git> |
 | Final PCBA on Altium 365 | <https://upenn-eselabs.365.altium.com/designs/C2F50C2C-DB4E-4CE0-9A4E-54B61E7DBE63> |

## 3. Hardware & Software Requirements

### Hardware Requirements Specification (HRS) Verification Review
The purpose of this section is to review the hardware requirements and constraints for the **`Pocket Star 1 (PS1)`**  star tracker system.

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| HRS-01 | The system shall utilize two servo motors defined as “servo motor 1” and “servo motor 2” | Instead of servo motors, the system utilized two stepper motors using the manufatured PCBA (this requirement change because the stepper motor capability to move in an expected degree); the boost circuit worked well; the system can only utilized stepper motors while connected to the Lithium Ion Battery due to current constraint of USB power source |
| HRS-02 | Servo motor 1 shall be controlled by the SAMD21 for x-axis movement | Requirement satisfied |
| HRS-03 | Servo motor 2 shall be controlled by the SAMD21 for y-axis movement | Requirement satisfied |
| HRS-04 | The system shall utilize a camera rig structure with 2 degrees of freedom | Requirement satisfied |
| HRS-05 | The system shall utilize a camera rig structure capable of mounting a camera weighing up to 1.5 lbs with dimension up to 120 x 85 x 45 mm|Due to stepper motor size limitation, the system only be able to mount a cellphone camera in our prototype; to be able to mount a larger camera, bigger stepper motor should be considered |
| HRS-06 | The x-axis shall have joint limit up to 180 degrees | Requirement satisfied |
| HRS-07 | The y-axis shall have joint limit up to 90 degrees | Requirement satisfied |
| HRS-08 | The servo motor input voltage shall not exceed 5 V, with current usage of 3 A<br><br>**NOTE:** This requirement intend to maintain the servo torque at 4.8V 13.5kg/cm with positioning speed of 4.8V, no-load 0.17s/60 degrees, as per fabrication specification | The stepper motor input voltage is approximately 4.8V as tested and measured in `A11G Board Bringup` asssignment |
| HRS-09 | The system shall run from a single cell Li-Ion battery (3.7V nominal voltage) | Requirement satisfied |
| HRS-10 | The system shall use the SAMW25 as the microcontroller and Wi-Fi communication IC | Requirement satisfied |
| HRS-11 | The system shall interface with the Quectel L76-L GPS module via I2C | Instead of the Quectel L76-L GPS module, we change the GPS module to ST Microelectronics Teseo LIV3R GPS/GNSS module; the functional is the same and this module is able to connect to the system via I2C |
| HRS-12 | The system shall have four LEDs defined as LED1, LED2, LED3, LED4 | The system has six LEDs instead; the requirements changed along the design process; two more LEDs are for Serial Communication status and Li-Po Charger Status|
| HRS-13 | LED1 shall be used to indicate when the system receives power | Requirement satisfied |
| HRS-14 | LED1 shall be a green LED | Requirement satisfied |
| HRS-15 | LED2 shall be used to indicate the polar alignment status | Requirement satisfied |
| HRS-16 | LED2 shall be a red LED | Requirement satisfied |
| HRS-17 | LED3 shall be used to indicate when polar alignment is complete and the current tracking status | Requirement satisfied |
| HRS-18 | LED3 shall be a blue LED | Requirement satisfied |
| HRS-19 | LED4 shall be used to indicate wifi connectivity status | Requirement satisfied |
| HRS-20 | LED4 shall be a yellow LED | Requirement satisfied |
| HRS-21 | The system shall have a single mechanical latching switch (Switch 1) | Requirement not satisfied for this prototype due to time constraint; it should be uncomplicated if it is required to be added in the future |
| HRS-22 | Switch 1 shall be used to indicate when to power on/power off the system | Requirement not satisfied for this prototype due to time constraint; it should be uncomplicated if it is required to be added in the future |
| HRS-23 | The system shall have two mechanical push buttons defined as Button 1 and Button 2 | Requirement satisfied |
| HRS-24 | Button 1 shall be used to indicate when to start the alignment | Requirement satisfied |
| HRS-25 | Button 2 shall be used to indicate when to start the tracking and when to interrupt the tracking process | Requirement satisfied |

### Software Requirements Specification (SRS) Verification Review
The purpose of this section is to review the software requirements and constraints for the **`Pocket Star 1 (PS1)`**  star tracker system.

#### Star Tracking Operation

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| SRS-01 | The system shall be able to locate the Polaris star based on latitude and longitude coordinates | The GPS coordinates require further refinement; the system is capable of locating the Polaris star, but further research on the accuracy of this system is required. We are somewhat limited by lack of orientation data. |
| SRS-02 | The system shall perform the polar alignment procedure based on its location relative to the Polaris star | The GPS coordinates require further refinement; further research on the accuracy of this system is required |
| SRS-03 | The system shall track an astronomical object for a specified time set by the user | Requirement satisfied |
| SRS-04 | The system shall start the polar alignment process once button 1 has been pressed | Requirement satisfied |
| SRS-05 | The system shall not start tracking if the polar alignment has not been completed | Requirement satisfied |
| SRS-06 | The system shall start tracking once the system is properly aligned and button 2 has been pressed | Requirement satisfied |
| SRS-07 | The system shall track astronomical objects at a sidereal rate | For this prototype, a sidereal rate that is defined as the rate at which stars move across the sky when viewing from Earth (approximately 15.042 arcseconds per second or 1/360th of a degree) is not satisfied; the prototype move the stepper motor angle of 1.8 degree per step; further research on the accuracy of this system is required |
| SRS-08 | During tracking operation, the system shall be rotating the camera counter clockwise | Requirement satisfied |
| SRS-09 | After tracking has completed, the system shall reorient the camera to its initial position before tracking was started | Requirement satisfied |
| SRS-10 | If button 2 is pressed while a tracking sequence is in-progress, the current tracking operation will be interrupted | Requirement satisfied |
| SRS-11 | The system should orient the camera in the direction of the desired astronomical object | The GPS coordinates require further refinement; further research on the accuracy of this system is required |

#### Data Acquisition

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| SRS-12 | The system shall be able to properly parse all fields of NMEA GPS messages | Requirement satisfied |
| SRS-13 | The system shall obtain its current latitude and longitude coordinates within ± 0.0001° <br><br> **NOTE**: This translates to roughly a variation in location of between 1.1m | Requirement satisfied |
| SRS-14 | New GPS data will be measured every 2 seconds | Requirement satisfied |
| SRS-15 | GPS data acquired will always maintain a quality level of 4 or 5 according to the NMEA protocol standard <br><br> **NOTE** A quality level of 4 (RTK Fixed) is centimeter precision and a quality level of 5 (RTX Float) is decimeter precision | Requirement satisfied |

#### Web Interface (Node-Red Dashboard)

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| SRS-16 | The system shall support communication between the embedded target and a web interface via WiFi | Requirement satisfied |
| SRS-17 | The web interface shall display the current latitude and longitude coordinates of the system | Requirement satisfied |
| SRS-18 | When tracking has started, the system shall display the remaining time left for tracking the astronomical object | Requirement satisfied |
| SRS-19 | The web interface shall display the current polar alignment status: <br> <ul><li>Not-aligned</li> <li> Aligned</li></ul> | Requirement satisfied |
| SRS-20 | The web interface shall display the current tracking status: <br> <ul> <li>Not-tracking</li> <li>Tracking</li> <li>Tracking-complete</li></ul> | Requirement satisfied |
| SRS-21 | The web interface should list the viewable astronomical objects from the system’s current position | Requirement satisfied |
| SRS-22 | The web interface/dashboard shall allow the user to specify or select what astronomical object they are tracking each tracking session through | Requirement satisfied |
| SRS-23 | The web interface shall allow the user to specify the desired duration of tracking for each session | Requirement satisfied |

**NOTE**: We ran into an issue where the data GNSS data acquired had floating point precision which we were able to verify through the in circuit debugger. However, we were unable to display that data in a readable format without first converting to an integer which removed noticeable precision from the displayed coorinates. THis does not impact the operation of the PS1 but any further development would benefit from solving this issue. 

#### Status Indicators

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| SRS-24 | When power is supplied to the system, LED1 should turn on | Requirement satisfied |
| SRS-25 | When power is removed to the system, all LEDs in the system shall turn off | Requirement satisfied |
| SRS-26 | When polar alignment starts, LED2 shall turn on | Requirement satisfied |
| SRS-27 | When polar alignment starts, LED3 shall turn off | Requirement satisfied |
| SRS-28 | When polar alignment is complete and correct, LED 2 shall turn off. | Requirement satisfied |
| SRS-29 | When polar alignment is complete and correct, LED 3 shall turn on | Requirement satisfied |
| SRS-30 | When the tracking begins, LED 3 shall begin flashing at a rate of 2 HZ | Requirement satisfied |
| SRS-31 | When the tracking completes all LEDs in the system shall turn on | Requirement satisfied |
| SRS-32 | When the system is connected to a wifi source, LED4 shall be lit | Requirement satisfied |
| SRS-33 | When the system is not connected to a wifi source, LED4 shall begin flashing at a rate of 2 HZ | Requirement satisfied |

#### Data Logging

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| SRS-34 | The system shall record and store session statistics in a json file | Requirement not satisfied |
| SRS-35 | The system shall store the follow metrics: <br> <ol> <li> Latitude at the time of tracking </li> <li> Longitude at the time of tracking </li> <li> Name of desired astronomical object to track </li> <li> Celestial coordinates oftracked astronomical object</li> <li>Duration of tracking </li></ol> | Requirement not satisfied |

## 4. Project Photos & Screenshots
### Final Project Prototype
#### Casework
#### Interfacing Elements
(3D prints, screens, buttons, etc.)

### PCBA
#### Highlight
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/07a96f42-7bb8-4038-abce-f55124b5c92d" alt="PCBA Highlight">

#### Standalone Top View
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/78cd7c80-48c9-4ebf-9d8c-6e3ba8819152" alt="Standalone Top View">

#### Standalone Bottom View
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/549ac357-bf85-441b-bac9-3dbf797248ff" alt="Standalone Bottom View">

#### Thermal Camera Images
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/ae9e10e5-8af2-4aa9-88a4-b46012b4c31b" alt="Thermal Camera Image">

*(The image is taken while the while the board is running under load)*

### The Altium Board Design
#### 2D View Top
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/d06536f3-3a93-4b75-aad7-3b2406f06738" alt="2D View Top">

#### 2D View Bottom
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/36a645a6-cfc5-46d0-a692-c82d71432955" alt="2D View Bottom">

#### 3D View Top
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/e3111fae-e633-46d5-890a-80d2c24be2b5" alt="3D View Top">

#### 3D View Bottom
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/3cf47b41-f259-4a68-84d3-14e497bb530c" alt="3D View Bottom">

### Node-RED
#### Node-RED Dashboard
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/59ab5c44-fb75-4f36-a234-2c07537a9ba7" alt="Node-RED Dashboard">

#### Node-RED Backend
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/fac13edf-3a87-415c-94b0-3ec169e4505c" alt="Node-RED Backend">

### Final System Block Diagram
### Simple Block Diagram
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/7cf1fafa-5598-46d7-bbc0-ae9fc5320804" alt="Simple System Block Diagram">

### Detailed Block Diagram
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/905ddb12-668e-4f96-a08b-f5ec5d82b2a6" alt="Detailed System Block Diagram">

## Product Gallery
<img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/0e488e23-3052-4194-80ee-d94aba92063a" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/05ce3618-06e6-46cf-b2a2-9f9cc89667ca" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/ceccee58-abdd-43df-83a4-776250d2ce02" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/e9faa614-0256-4b32-ab1b-30e646db941b" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/406ad155-1fd6-49d9-81f4-7ad5e98dc6c3" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/4ac30298-735f-4990-bfc5-6ffeb34a9b82" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/bb2a01c4-360d-4e2f-8f36-713a3a7d397d" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/59bf10da-67a1-4d53-85d4-f9332390d206" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/814bb61b-0e67-44a3-b144-bbaefb0b3ead" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/e9051b58-8217-47b4-9fed-8482b9ce8bee" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/91fdd508-cd32-4689-a078-7ef758e7150e" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/ad9b3b21-acd4-4142-8beb-2d844b0e9c3d" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/dca68fe2-a372-4dea-b093-39c2a3c89432" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/02de4618-22af-4324-bdd8-1ddd66b01938" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/0085febc-be3c-4c94-ad65-60c6f5d908ef" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/4e5431e2-9b23-4165-9767-1c9cf62ede20" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/96328b09-e540-4458-b099-115d3d2da16b" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/caa1069d-adc0-4c40-9611-932cd6b61c60" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/165c9b50-52fd-4727-b93d-625d297f0c96" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/0d3913e0-5c40-4eb3-99ed-32c00de478f9" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/d6ac01ca-e6b3-4fb5-8696-e7ca40448b97" width="15%"></img> <img src="https://github.com/ese5160/a14g-final-submission-t04-ad-astra/assets/145785615/0332c747-cc94-4851-965f-d1fbe06f08c2" width="15%"></img> 