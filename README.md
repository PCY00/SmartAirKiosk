# SmartAirKiosk

## Language Selection

[English](README.md) | [Korean](README_KR.md)

<br><br>

## Overview

- Due to the rise in fine dust, the demand for masks has increased.
- It is difficult to eat while wearing masks in stores.
- As a result, staff members have to manage the store.
- If the store is busy, it becomes difficult to manage in real-time.
- Therefore, we developed a self-service kiosk that controls temperature, humidity, and fine dust to keep the store comfortable.

<br><br>

## Considerations

- The severity of fine dust today.
- Maintaining comfort in the store in real-time.
- The necessity of kiosks in stores (economic perspective -> kiosks are essential these days, so additional functions are implemented).

<br><br>

## Installation Photo

<div align="center">
  
  | Real Image |
  |:---:|
  | <img src="https://github.com/user-attachments/assets/314c94d4-e6bc-4acf-934e-5a8bf56400b1" width="350px" height="470px" alt="Real Image"> |
</div>

<br><br>

## SmartAirKiosk Operation Video

[Watch SmartAirKiosk Operation Video](https://youtu.be/KF5rC-BnxO0)

<br><br>

## Directory Structure

```
SmartAirKiosk/
├── APP/
│   ├── APP.jpg
│   ├── PMS_Alarm.jpg
│   │
├── GUI/
│   ├── gui.py
│   │
├── Sensor/
│   ├── RaspberryPi_3_PMS.py
│   ├── Temp_relay.cpp
│   ├── 초음파_PIR.cpp
│ 
├── Wiring/
│   ├── Wiring.jpg
│   │
├── modeling/
│   ├── SmartAir.png
│   ├── modeling.step

```

<br><br>

## Hardware Used

| Device                | Specifications                                                                                                                                                                                                                                                                                                                                                                     | Quantity | Remarks                         |
|:------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---:|:--------------------------:|
| Raspberry Pi 3B+   | Quad-core ARM® Cortex-A53 64-bit SoC @ 1.4GHz                                                                                                                                                                                                                                                                                                                                    | 3  |                            |
| HC-SR501  | Human motion sensor                                                                                                                                                                                                                                                                                                                                                              | 1  | Human motion sensor       |
| HC-SR04        | Ultrasonic sensor                                                                                                                                                                                                                                                                                                                                                              | 1  | Ultrasonic sensor                  |
| PMS7003            | Light scattering method                                                                                                                                                                                                                                                                                                                                              | 1  | Fine dust sensor                    |
| D06A0 Coolgen Circulator              |                         5V, 0.5A                                                                     |  1  | Fan |
| Arduino Relay Module            | Relay module                                                                                                                                                                                                                                                                                                                                                                     | 1  | Relay                     |
| 7-inch Display                 |   5V  |  1  |                 For touch display           |

<br><br>

## System Architecture

![System Architecture](https://github.com/user-attachments/assets/4c321007-3b18-4ea9-813b-6ff5827f3be3)

<br><br>

## Wiring Diagram

<div align="center">

  | Sensor Wiring | 
  |:---:|
  | <img src="https://github.com/user-attachments/assets/54dacca4-ecc6-4a91-9701-8f52dfa73992"  alt="Sensor Wiring Diagram"> |
</div>

<br><br>

## App Implementation

### MIT Inventer
- GET from Mobius
![2](https://github.com/user-attachments/assets/222d7ba7-0c47-4178-98b9-6ba8fb2832dc)

- POST to Mobius
![3](https://github.com/user-attachments/assets/257c163b-d529-4cd9-8b1f-c43a9f388afe)

<br><br>

## Features

### Card Registration Check
- Reads the UID value from the RFID reader and checks if it is registered in Mobius.
- If registered, deducts the payment amount from the card balance (if insufficient, a message will be displayed).
- If the UID is not registered, it outputs "invalid card."

### Kiosk Human Detection
- Uses PIR and ultrasonic sensors to detect people.
- Due to PIR's performance issues, ultrasonic sensors are used.
- A 5-second delay is applied considering the time a person leaves.

### Fan (Air conditioner in simulation) Control
- Automatically turns on the fan when the surrounding temperature exceeds 25°C.
- If the temperature falls below 25°C, the fan turns off.

### Fine Dust Management
- Uses the Air Korea API to compare external and internal fine dust concentrations.
- If the internal fine dust level is higher than the external level, the app sends a notification to open the window.
