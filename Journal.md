---
title: "RoverDrive Hardware"
author: "Dylan Itoh"
description: "A PCB for a robot"
created at: "2025-06-24"
---
### Total time: about 27 hours
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
Started doing the gyro/accelerometer for the robot. The robot will need to know the direction it is facing. some options are the mpu9250 and icm 20948, but you need to do extra complex stuff to calculate its orientation. 
While researching these, I saw the bno055 sensor which is very accurate, but there arent very many pictures of schematics I could find for reference. I have been looking at the schematic in its datasheet and also the schematic of the Adafruit breakout board

## Time Spent:  4 hours

## Day 5 - 6/29
Finished the imu schematic:

![Screenshot 2025-07-05 154006](https://github.com/user-attachments/assets/4f6e5530-e5e4-4977-a32b-592f3de0dd47)

All thats left is to add the connectors for sensors and servos and an led. 

I added 6 3-pin connectors (one for each 5v wheel servo, one for a tiny grabber arm servo, and another for a some extra 3.3v sensor), then I added a 4-pin connector for a distance sensor and a 2-pin connector for a controllable LED. 
It looks like this:
![Screenshot 2025-07-05 172137](https://github.com/user-attachments/assets/5a2cb900-a91b-4899-b077-4f6181e9f184)

## Time Spent:  2 hours

## Day 6 - 6/30
The schematic is done, now I'm picking the footprints.

I decided to remove the entire charging circuit because it's too complex and is just unnecessary. I realized I usually just replace the dead battery with a charged one because I need to use it continuously.
## Time Spent:  3 hours

## Day 7 - 7/1
I need to make the PCB now. It must fit within a space of 45mmx67mm and should have all connectors (except for wheel and battery) inside the orange area, like shown: 
![Screenshot 2025-07-05 192340](https://github.com/user-attachments/assets/75ef95b1-cd66-46c0-b914-46fa58445d65)

I placed all of the parts on the board. All the power components are all at the bottom. The esp32 sticks out of the side. I also tried to put all of the gyro parts in the center of the board so it is more accurate. The wheel servo headers and battery connectors are on the other side. It looks like this: 

![Screenshot 2025-07-05 235741](https://github.com/user-attachments/assets/d2d02d1e-b529-47e3-ba77-1929050e51f6)

I learned how to add ground planes to the pcb, so I added it to both sides.

I started the 5v power traces at the battery and made it super thick, around 1mm to 1.5mm.

Then, I did the 3.3v power traces, which goes from the regulator to the ESP module and all of the sensors. Both traces had to be routed along the side of the board because there wasnt much space.

I finally connected all of the signal pins. They had to go on both sides and needed vias. I also noticed that the ground plane got split up in many areas, so vias were needed to connect it to the other side
## Time Spent:  5 hours

## Day 8 - 7/2
The PCB is almost done, so I ran a design rules checker. It told me a bunch of the gnd pads werent right, so I added vias on them. Also, a bunch of wires were not connected yet, so I fixed them.

I moved all of the silkscreen stuff in better places to get rid of most of the warnings.

I learned how to add images on the silkscreen, so I added a few.

Its finished

![Screenshot 2025-07-06 183929](https://github.com/user-attachments/assets/b4f2685f-718c-4603-bfea-2713ab364a26)

## Time Spent:  1 hour

## Day 9 - 7/23
multiple changes had to be made to the CAD model to make the PCB fit well inside it:
- all of the old inside stuff was removed
- a hole was added to the side of the base for the ESP to stick through
- supports added to the edge of the base inside for the board to rest on
- top lid of the body had to be modified to prevent it from colliding with components on the PCB
- holes added in the top lid for connectors and the reset+boot buttons
- side connector holes moved around to make space for switch
- hole and support added for a power switch on the side of the base
- door added to the bottom of the base for easy battery access

Before:

<img width="492" height="293" alt="Screenshot 2025-07-23 234520" src="https://github.com/user-attachments/assets/3b85b5ac-cfd0-494c-9263-8938746d86cd" />

After: 

<img width="275" height="323" alt="image" src="https://github.com/user-attachments/assets/40328c8d-2542-44f9-ac91-9b1394e10a77" />


## Time Spent:  3 hours


## Assembly

## 7/18-19
I got all of the components and the pcb, so all that's left to do is solder everything. First, I attached all of the capacitors, then resistors, then all of the power supply components and battery plug. I wanted to test if it powered up, and I ran into a big problem. After plugging the battery in, it heated up and the regulator components started smoking. Using a multimeter, I found that there was a short between 5v and gnd. I decided it was best to keep removing components until it stopped showing continuity. It turned out to all be caused by the 100nf capacitors, which for some reason had continuity between both ends. Maybe I got the wrong type. I decided to move on without battery power and focus on the actual microcontroller. I used a heat gun and solder paste to attach the IMU, which was kind of hard and took a few tries. Soldering the ESP was almost impossible, but I attached it by heating from the bottom. I soldered the usb receptacle last, and it got kind of melty. When plugging it in, it got power, but would not show up as a device       

## 7/28
I continued working on the pcb.

I assumed it was the bad soldering of the ESP that caused the problem. Or maybe I cooked the ESP after it being under the heat gun for so long. I unsoldered the module from the board and instead attached it using many thin wires. It might not look nice, but it should work.
After powering it on, It did not work. still the exact same as before.

## 8/1
I came up with another idea that it might be the USB port that was not soldered well. I noticed that the pads of the receptacle were all lifted up, except for the power ones, and were also super bent up. I replaced it with a port desoldered from a different board and made sure to press it down while soldering it on.

I probed around again with a multimeter to see if there were any issues. The data lines were connected to the USB, and were not connected to each other. After plugging it in, it still did not show as a device. I thought I might need to uploed firmware to activate it somehow, but I do not know how.

## 8/2
I started messing with the board again with a multimeter, and discovered that the ESP module wasn't even recieving power. The problem was really just the vcc wire accidentally being soldered to gnd. After fixing this one thing, the board actually worked and connected to the computer. It often disconnected though, and I assumed it was still the usb connector not soldered well. I pressed it to the board while heating it with a heat gun, and the issue dissapeared when plugging it in.
