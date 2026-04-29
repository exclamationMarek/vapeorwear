# VAPEorWEAR
Wearable SAO power pack

![](images/render.png)

Designed around a battery, that is upcycled from a single use vape, that a friend of mine found (in worryingly large quantities!) in the recycling room of his house. It features a proper battery charger and protection IC, so that the poor, abused lithium cell can now live a comfortable afterlife powering your shitty add ons.

# Features
## Wearable
* 2x M4 holes that should fit lanyard clips
* Rounded edges and no poking-out THT pins on the backside, to not ruin your nice t-shirt

## 400mAh upcycled battery
* It might smell like fruity vape juice

## [RY2201](https://www.lcsc.com/datasheet/C370889.pdf) battery protection IC
* Overcharge protection at 4.3V
* Overdischarge protection at 2.4V
* Overcurrent protection at 3.0A

## [BRCL4054CME](https://www.lcsc.com/datasheet/C305436.pdf) battery charger
* CCCV charging to 4.2V
* R11 sets charging current. Recommended 5.1k gives 196mA (2.5h charge time)
* CHRG led will shine during charging, and gently glow when done

## [MT3406](https://www.lcsc.com/datasheet/C22462728.pdf) buck converter
* Efficiently produces 3.3V from VBAT
* 1A output continuous, 2A self-protected limit
* Paired with [INPAQ WIP252012P-4R7ML](https://www.lcsc.com/datasheet/C964123.pdf) inductor (4.7µH, 1.9A ISat, 196mΩ)
* Not a boost-buck, so output voltage will start dropping as VBAT drops below 3.4V

## [ON/OFF switch](https://www.lcsc.com/datasheet/C22435662.pdf) and PWR LED
* Switch controls the ENABLE pin of the buck converter
* LED is connected to the 3.3V rail
* Quiescent current when OFF < 3µA
* Quiescent current when ON approx. 150µA
* Most of the Quiescent ON current is the PWR led, remove it to drop to 30µA

## [USB-C port](https://www.lcsc.com/datasheet/C42400650.pdf) for 5V input
* Includes 5.1k resistors to actually work with USB-C chargers

## 31 x 13mm battery cavity
* With 4x 3x1.5mm zip-tie or tape slots for mounting
* Prominently shows the battery, no mechanical cell protection offered
* JST-ZH (1.5mm) 2-pin connector

## 2.54mm pin row for connecting to the SAO
* breaks out all SAO pins, and 5V and extra GND
* VCC, GND and I2C pins are arranged so that an I2C OLED (example SSD1306) can be connected directly, should the SAO feature a micro and wish to display something.


# Assembly instruction
For your convenience, most components are arranged in simple rows. The recommended order of soldering is, row by row, and each row is listed **from left to right**

![](images/assembly.png)

## ROW 1: LEDS
Negative (stripe) always faces left
1. Yellow LED (charging indicator)
2. Yellow LED (power indicator)

## ROW 2: LED resistors
1. 5.1k (sets brightness of charging LED)
2. 5.1k (sets brightness of power LED)

## ROW 3: ICs
Pin 1 (dot) is always bottom right
1. BRCL4054CME (battery charger)
2. MT3406 (buck converter)
3. RY2201 (battery protection)

## ROW 4: Capacitors
1. 1uF
2. 22uF
3. 22uF
4. 22uF (optional)
5. 1uF

## ROW 5: Resistors
1. 5.1k	(charge current set resistor)
2. 47k	(VOUT set resistor 1)
3. 220k	(VOUT set resistor 2)
4. 220k	(Buck converter ENABLE pull-up)
5. 100R	(Battery protection power filter)

## Remaining components:
Its position and orientation has been left as an exercise to the assembler
1. 4.7uH inductor next to the buck converter
2. On-off switch
3. Battery connector
4. USB-C port
5. 2x 5.1k resistors near the USB-C port
6. SAO connector. Unkeyed, sorry!

# Post assembly test
1. Do not plug in battery yet!
2. Plug in USB power source and test if:
	* VBAT reads approx. 4.2V
	* 3.3V reads approx. 3.3V
3. Check polarity of battery cable. Left pin should be positive
4. If so, you can unplug the usb, plug in the battery and enjoy your VAPEorWEAR

# Other notes
* There is a non-zero chance that you received the kit with "5.1k" resistors actually being 4.99k, because those are the ones I had a spool off. Similarly the 100R might be a 120R or something. Should still work.