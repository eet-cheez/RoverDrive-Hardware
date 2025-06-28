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

![Screenshot 2025-06-28 012638](https://github.com/user-attachments/assets/57f5827b-4c7f-4461-9a74-318bac3df5ff)

Because the power is on 5v, i needed to add a voltage regulator. AMS1117-3.3 is very common, so i used it.

## Time Spent: 3 hours

## Day 3 - 6/26
now, I need to do the battery charging. I normally use a 2 cell lithium battery, but I'll switch to a single cell lipo because the circuit is probably simpler. the most common charging IC is the tp4056




## Time Spent:  hours
