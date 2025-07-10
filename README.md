# RoverDrive-Hardware
A custom PCB for a robot powered by an esp32 microcontroller that has pins to control 4 servos plus one for sub-micro servo at 3.3v (in case it burns out at 5v). It also can support multiple other devices like LEDs or sensors and has an IMU to know its direction.

![Screenshot 2025-07-09 000034](https://github.com/user-attachments/assets/36470689-e1ac-4909-b196-7ea8482a30d5)
![Screenshot 2025-07-09 005853](https://github.com/user-attachments/assets/a746ac2a-13a0-4acd-abf8-00fe2f0e954b)
![Screenshot 2025-07-09 005949](https://github.com/user-attachments/assets/760a9857-7d93-4117-ad8f-c38bcb594ffb)


### Why am I doing this?
Last year, I built a robot that was controlled by connecting to an app. The problem is that the inside was a mess of wires and modules floating around, so it was a pain to fix and improve. I decided a PCB could fit more features while also being much easier to assemble and access.

## Details
- The microcontroller is an ESP32-S3-mini-1. I only really chose it because it seemed compact, but there are probably much better options. 
- For the IMU, it uses a BNO055, which does all of the calculations internally to find its orientation. Might be a bit overkill, but I want to make sure it works properly.
- The board uses a basic ams1117-3.3 to to power all of the 3.3v devices.
- Power is supplied to the board via a 1s lipo battery, which gets boosted to 5v by a mt3608 regulator.
- PCB designed in KiCad.
### Schematic: 
![Screenshot 2025-07-09 000448](https://github.com/user-attachments/assets/8ccad17f-91cd-48b2-979c-726ddea5a343)
### PCB: 
![Screenshot 2025-07-06 183929](https://github.com/user-attachments/assets/1a3bf91a-3b2b-44f1-b272-d67cc10cb875)

This is that the robot looks like with a model of the PCB (in TinkerCad):
 
![Screenshot 2025-07-09 001057](https://github.com/user-attachments/assets/1672e596-b73b-4b48-82c0-f60903a756ec)

## BOM
| Item                  | Description         | Quantity | Cost |
|-----------------------|---------------------|----------|----------------|
|ESP32-S3-MINI-1-N8|	the microcontroller	|1	|$6.15 |
|NFM18PC104R1E3D|	100nf capacitor	|13	|$1.69|
|PTS647SN50SMTR2 LFS|	reset and boot buttons|	2	|$0.46|
|GRM188C81A226ME01D|	22uf ceramic capacitor|	3	|$0.87|
|TAJA226K010RNJ|	22uf tantalum capacitor. for ams1117-3.3	|2|$0.70|
|SS34| schottky diode	|1|$0.52|
|SRP7028AA-220M|	22uh inductor	for 5v regulator|1|$1.11|
|C1608X7T1A106M080AC|	10uf ceramic capacitor	|3|	$0.69|
|06031A220FAT2A|	22pf ceramic capacitor for gyro|3	|$1.32|
|CRCW060310K0FKEI|	10k resistor	|7	|$1.05|
|CRCW06035K10FKEC|	5.1k resistor	|3	|$0.36|
|RNCE0603BTE1K00|	1k resistor	|2|$0.42|
|ERJ-3RBD7501V|	7.5k resistor	|2|$0.30|
|ABS07-32.768KHZ-7-T|	32.768 kHz crystal for gyro|1|$0.82|
|BNO055|	9 axis IMU	|1|$12.34|
|USB4105-GF-A	|USB c receptacle, 16 contact|1|$0.78|
|MT3608|	boost converter. used to increase battery voltage to 5v (already have)|	1	|$0|
|AMS1117-3.3|	3.3v voltage regulator	|1	|$0|
|2.54mm pin headers	|for servos	|5| $0|
|Molex picoblade connector|fits with the battery, probably|1|$0|
|JST Connectors (2-pin, 3-pin, 4-pin)|Probably JST XH|3|$0|
|PCB|from JLCPCB|1|$41.71 **(See below for price explanation)***|
**Total:			$71.29**

Sheet with part links: https://docs.google.com/spreadsheets/d/1vR1n98YzZK8dJmbvGAbjTAVUf36cDbNLpNew4ql-z88/edit?usp=sharing

### * PCB Price Explanation
I'm exhibiting the full Roverdrive project at Open Sauce this year and did not have much time to create the hardware (need to finish by the 19th, difficult with Undercity taking up time). In order to get the PCB on time, I had to pay way more for shipping and couldn't spend much time optimizing the cost. I've already bought all of the parts, and I understand if Hack Club doesn't want to reimburse the full cost. If needed, I would gladly take a smaller, more reasonable reimbursement.
