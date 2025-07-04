---
title: "RoverDrive Hardware"
author: "Dylan Itoh"
description: "Purpose is to improve and organize the electronics inside the 'RoverDrive' robot by designing one PCB for everything"
created_at: "2025-06-24"
---

# Journal

## Day 1 - 6/24
I mostly spent this time planning what features the control board needs. It must be able to connect to to an app, have many pins for sensors, leds, and servos, and possibly add new stuff like gyro and battery charging.
I think I might use an esp32 s3 mini module.
## Time Spent: 1 hour

## Day 2 - 6/25
Started on the schematic for the microcontroller part. I have never really done this before so I watched some tutorials.
![Screenshot 2025-06-28 010405](https://github.com/user-attachments/assets/2e44fa90-5cc0-4802-bacb-7e78f1422c7d)
I added reset and boot button circuits, some caps on its 3.3v input, and a usb c connector.

![Screenshot 2025-07-02 164555](https://github.com/user-attachments/assets/472cbe6f-9b1e-455d-9863-729c40cb590b)

Because the power is on 5v, i needed to add a voltage regulator. AMS1117-3.3 is very common, so i used it.

## Time Spent: 3 hours

## Day 3 - 6/26
now, I need to do the battery charging. I normally use a 2 cell lithium battery, but I'll switch to a single cell lipo because the circuit is probably simpler. Then I made the circuit by looking at a video and the datasheets of each part.
![Screenshot 2025-07-02 122613](https://github.com/user-attachments/assets/c70e7822-7478-4de9-950b-1fa0707f86c4)

It uses a separate usbc connector for charging. has tp4056 as the carging IC, a fs312f for protection, and an mt3608 for boosting it to 5v. I also added two empty wire holes for a switch

## Time Spent:  5 hours

## Day 4 - 6/28
Started doing the gyro/accelerometer for the robot. The robot will need to know the direction it is facing. some options are the mpu9250 and icm 20948, but you need to do extra complex stuff to calculate its orientation. while researching these, I saw the bno055 sensor which is very accurate.
There arent very many pictures of schematics I could find for reference. I have been looking at the schematic in its datasheet and also the schematic of the Adafruit breakout board

## Time Spent:  4 hours
