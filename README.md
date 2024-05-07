[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/kzkUPShx)
# a14g-final-submission

    * Team Number: 4
    * Team Name: Ad Astra
    * Team Members: Miles Osborne & Oryza Tarigan
    * Github Repository URL: https://github.com/ese5160/a14g-final-submission-t04-ad-astra.git
    * Description of test hardware: Windows 10 Laptop, Atmel SAMD21 Microcontroller Unit + ATWINC1500B Wifi Module, Ad Astra - Pocket Star 1 (PS1) PCBA, GPS Sensor (ST Microelectronics Teseo LIV3R GPS/GNSS), GNSS / GPS Development Tools GNSS expansion board based on Teseo-LIV3F module for STM32 Nucleo (STMicroelectronics 511-X-NUCLEO-GNSS1A1), Bipolar Stepper Motor Hybrid Frame Size 11 200.0 Step 670 mA 4.56VDC (Pololu 1206)

## 1. Video Presentation

## 2. Project Summary

### Device Description
The device is called **`Pocket Star 1 (PS1)`** which is a “smart” star tracker. A star tracker is a tool used in astrophotography to help align the camera’s lens with the Earth’s rotation and follow the target’s path.

The device capable of doing configuration to adjust the rate and for how long it tracks the object and an auto-polar alignment feature as an essential feature.

Additional features are also centered around user input and feedback. Through a user interface such as Node-Red, we shall allow users to select what star or astronomical object they would like to view before the tracking starts and display statistics such as time remaining for the current tracking session. Lastly, for the wireless connectivity aspect of the system, we shall support over-the-air firmware updates in the case that we have to make changes in the field or outside of development.

### Inspiration
Traditionally, every star tracker requires polar alignment before it can be used each time. This is usually a manual process that can take a few minutes to get right. Similarly, many star trackers allow for some form of configuration to adjust the rate and for how long it tracks the object. This device intends to replicate some of these functions (on a smaller scale) but also automate some of the manual aspects involved with the process. To the best of our knowledge, this has not been a feature incorporated on any star tracker currently available for purchase.

### Device Functionality
- Explain how your Internet-connected device is designed
- Include sensors, actuators, and other critical components.
- Your block diagram from earlier in this semester will be quite helpful here!

### Challenges
- Where did you face difficulties? This could be in firmware, hardware, software, integration, etc.
- How did you overcome these challenges?

### Prototype Learnings
- What lessons did you learn by building and testing this prototype?
- If you had to build this device again, what would you do differently?

### Next Steps
- What steps are needed to finish or improve this project?

### Takeaways from ESE5160
- What did you learn in ESE5160 through the lectures, assignments, and this course-long prototyping project?

### Project Links
Some project links for review are listed below.
 | Description | URL |
 | ----------- | --- |
 | Node-RED Dashboard | http://20.81.250.63:1880/ui |
 | Node-RED Backend | http://20.81.250.63:1880 |
 | Final Embedded C Firmware Codebases (A12G Code Repository) | https://github.com/ese5160/a12g-firmware-drivers-t04-ad-astra.git |
 | Node-RED Dashboard Code (A12G Code Repository) | https://github.com/ese5160/a12g-firmware-drivers-t04-ad-astra.git |
 | Final PCBA on Altium 365 | https://upenn-eselabs.365.altium.com/designs/C2F50C2C-DB4E-4CE0-9A4E-54B61E7DBE63 |

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
| SRS-01 | The system shall be able to locate the Polaris star based on latitude and longitude coordinates | The GPS coordinates require further refinement; the system is capable of locating the Polaris star, but further research on the accuracy of this system is required |
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
| SRS-20 | The web interface shall display the current tracking status: <br> <ul> <li>Not-tracking</li> <li>Tracking</li> <li>Tracking-complete</li></ul> | Requirement satisfied partially; the system only show whether the tracking is on going or not |
| SRS-21 | The web interface should list the viewable astronomical objects from the system’s current position | Requirement satisfied |
| SRS-22 | The web interface/dashboard shall allow the user to specify or select what astronomical object they are tracking each tracking session through | Requirement satisfied |
| SRS-23 | The web interface shall allow the user to specify the desired duration of tracking for each session | Requirement satisfied |

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
| SRS-34 | The system shall record and store session statistics in a json file | Requirement satisfied |
| SRS-35 | The system shall store the follow metrics: <br> <ol> <li> Latitude at the time of tracking </li> <li> Longitude at the time of tracking </li> <li> Name of desired astronomical object to track </li> <li> Celestial coordinates oftracked astronomical object</li> <li>Duration of tracking </li></ol> | Requirement satisfied |

## 4. Project Photos & Screenshots
### Final Project Prototype
#### Casework
#### Interfacing Elements
(3D prints, screens, buttons, etc.)

### PCBA
#### Highlight
![Highlight](/images/Lightbox%20Photo.JPG)
#### Standalone Top View
![Standalone Top View](/images/Standalone%20Top%20View.jpg)
#### Standalone Bottom View
![Standalone Bottom View](/images/Standalone%20Bottom%20View.jpg)
#### Thermal Camera Images
![Thermal Camera Image](/images/PCBA%20Under%20Load.jpeg)

*(The image is taken while the while the board is running under load)*

### The Altium Board Design
#### 2D View Top
![2D View Top](/images/PCBA%202D%20Top.png)
#### 2D View Bottom
![2D View Bottom](/images/PCBA%202D%20Bottom.png)
#### 3D View Top
![3D View Top](/images/PCBA%203D%20Top.png)
#### 3D View Bottom
![3D View Bottom](/images/PCBA%203D%20Bottom.png)

### Node-RED
#### Node-RED Dashboard
#### Node-RED Backend


### Final System Block Diagram
### Simple Block Diagram
![Simple System Block Diagram](/images/Simple%20System%20Block%20Diagram_Final.jpg)
### Detailed Block Diagram
![Detailed System Block Diagram](/images/Detailed%20System%20Block%20Diagram_Final.jpg)