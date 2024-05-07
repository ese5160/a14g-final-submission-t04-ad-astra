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
- What problem is your device solving? How do you use the Internet so augment your device functionality?

### Inspiration
- What inspired you to do the project?

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
- Provide a URL to your Node-RED instance for our review (make sure it’s running on your Azure instance!)
- Include a link to your A12G code repository
    - Do NOT put your code in the A14G assignment’s repository. 
    - The A12G repository must include your final embedded C firmware codebases and Node-RED dashboard code.
    - Your code will be evaluated for its driver implementations, application code, OTAU approach, comments, and cleanliness.
    - If any open source code was used in your project, it must be referenced and used according to its licensing information. If you heavily leveraged tools, websites, or the expertise of others, this must be noted in the Github Readme.
- Provide the share link to your final PCBA on Altium 365.
    - Consider downloading your PCBA source and manufacturing files to keep after you leave UPenn. Your Altium access will expire after this semester.

## 3. Hardware & Software Requirements

### Hardware Requirements Specification (HRS) Verification Review
The purpose of this section is to review the hardware requirements and constraints for the **`Pocket Star 1 (PS1)`**  star tracker system.

|Req ID|Requirement|
|------|-----------|
|HRS-01|The system shall utilize two servo motors defined as “servo motor 1” and “servo motor 2”|
|HRS-02|Servo motor 1 shall be controlled by the SAMD21 for x-axis movement|
|HRS-03|Servo motor 2 shall be controlled by the SAMD21 for y-axis movement|
|HRS-04|The system shall utilize a camera rig structure with 2 degrees of freedom|
|HRS-05|The system shall utilize a camera rig structure capable of mounting a camera weighing up to 1.5 lbs with dimension up to 120 x 85 x 45 mm|
|HRS-06|The x-axis shall have joint limit up to 180 degrees|
|HRS-07|The y-axis shall have joint limit up to 90 degrees|
|HRS-08|The servo motor input voltage shall not exceed 5 V, with current usage of 3 A<br><br>**NOTE:** This requirement intend to maintain the servo torque at 4.8V 13.5kg/cm with positioning speed of 4.8V, no-load 0.17s/60 degrees, as per fabrication specification|
|HRS-09|The system shall run from a single cell Li-Ion battery (3.7V nominal voltage)|
|HRS-10|The system shall use the SAMW25 as the microcontroller and Wi-Fi communication IC|
|HRS-11|The system shall interface with the Quectel L76-L GPS module via I2C|
|HRS-12|The system shall have four LEDs defined as LED1, LED2, LED3, LED4|
|HRS-13|LED1 shall be used to indicate when the system receives power|
|HRS-14|LED1 shall be a green LED|
|HRS-15|LED2 shall be used to indicate the polar alignment status|
|HRS-16|LED2 shall be a red LED|
|HRS-17|LED3 shall be used to indicate when polar alignment is complete and the current tracking status|
|HRS-18|LED3 shall be a blue LED|
|HRS-19|LED4 shall be used to indicate wifi connectivity status|
|HRS-20|LED4 shall be a yellow LED|
|HRS-21|The system shall have a single mechanical latching switch (Switch 1)|
|HRS-22|Switch 1 shall be used to indicate when to power on/power off the system|
|HRS-23|The system shall have two mechanical push buttons defined as Button 1 and Button 2|
|HRS-24|Button 1 shall be used to indicate when to start the alignment|
|HRS-25|Button 2 shall be used to indicate when to start the tracking and when to interrupt the tracking process|

### Software Requirements Specification (SRS) Verification Review
The purpose of this section is to review the software requirements and constraints for the **`Pocket Star 1 (PS1)`**  star tracker system.

#### Star Tracking Operation

| Req ID | Requirement |
| ------ | ------ |
| SRS-01 | The system shall be able to locate the Polaris star based on latitude and longitude coordinates                         |
| SRS-02 | The system shall perform the polar alignment procedure based on its location relative to the Polaris star                        |
| SRS-03 | The system shall track an astronomical object for a specified time set by the user                                      |
| SRS-04 | The system shall start the polar alignment process once button 1 has been pressed                                       |
| SRS-05 | The system shall not start tracking if the polar alignment has not been completed                                       |
| SRS-06 | The system shall start tracking once the system is properly aligned and button 2 has been pressed                       |
| SRS-07 | The system shall track astronomical objects at a sidereal rate                                                         |
| SRS-08 | During tracking operation, the system shall be rotating the camera counter clockwise                                    |
| SRS-09 | After tracking has completed, the system shall reorient the camera to its initial position before tracking was started |
| SRS-10 | If button 2 is pressed while a tracking sequence is in-progress, the current tracking operation will be interrupted    |
| SRS-11 | The system should orient the camera in the direction of the desired astronomical object                                 |

#### Data Acquisition

| Req ID | Requirement  |
| ------ | ------ |
| SRS-12 | The system shall be able to properly parse all fields of NMEA GPS messages |
| SRS-13 | The system shall obtain its current latitude and longitude coordinates within ± 0.0001° <br><br> **NOTE**: This translates to roughly a variation in location of between 1.1m |
| SRS-14 | New GPS data will be measured every 2 seconds |
| SRS-15 | GPS data acquired will always maintain a quality level of 4 or 5 according to the NMEA protocol standard <br><br> **NOTE** A quality level of 4 (RTK Fixed) is centimeter precision and a quality level of 5 (RTX Float) is decimeter precision |

#### Web Interface (Node-Red Dashboard)

| Req ID | Requirement |
| ------ | ------ |
| SRS-16 | The system shall support communication between the embedded target and a web interface via WiFi                                                |
| SRS-17 | The web interface shall display the current latitude and longitude coordinates of the system                                                   |
| SRS-18 | When tracking has started, the system shall display the remaining time left for tracking the astronomical object                               |
| SRS-19 | The web interface shall display the current polar alignment status: <br> <ul><li>Not-aligned</li> <li> Aligned</li></ul>                       |
| SRS-20 | The web interface shall display the current tracking status: <br> <ul> <li>Not-tracking</li> <li>Tracking</li> <li>Tracking-complete</li></ul> |
| SRS-21 | The web interface should list the viewable astronomical objects from the system’s current position                                             |
| SRS-22 | The web interface/dashboard shall allow the user to specify or select what astronomical object they are tracking each tracking session through |
| SRS-23 | The web interface shall allow the user to specify the desired duration of tracking for each session                                            |

#### Status Indicators

| Req ID | Requirement                                                                                    |
| ------ | ---------------------------------------------------------------------------------------------- |
| SRS-24 | When power is supplied to the system, LED1 should turn on                                      |
| SRS-25 | When power is removed to the system, all LEDs in the system shall turn off                     |
| SRS-26 | When polar alignment starts, LED2 shall turn on                                                |
| SRS-27 | When polar alignment starts, LED3 shall turn off                                               |
| SRS-28 | When polar alignment is complete and correct, LED 2 shall turn off.                            |
| SRS-29 | When polar alignment is complete and correct, LED 3 shall turn on                              |
| SRS-30 | When the tracking begins, LED 3 shall begin flashing at a rate of 2 HZ                         |
| SRS-31 | When the tracking completes all LEDs in the system shall turn on                               |
| SRS-32 | When the system is connected to a wifi source, LED4 shall be lit                               |
| SRS-33 | When the system is not connected to a wifi source, LED4 shall begin flashing at a rate of 2 HZ |

#### Data Logging

| Req ID | Requirement |
| ------ | ------ |
| SRS-34 | The system shall record and store session statistics in a json file |
| SRS-35 | The system shall store the follow metrics: <br> <ol> <li> Latitude at the time of tracking </li> <li> Longitude at the time of tracking </li> <li> Name of desired astronomical object to track </li> <li> Celestial coordinates oftracked astronomical object</li> <li>Duration of tracking </li></ol> |

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


### System Block Diagram