# HyperDrive

Flite Test is doing a build video on the HyperDrive that Jesse Perkins and I built for their Whoop Course at Edgewater Airpark. This GitHub is in support of that video.

# Electronics Build
**Electronic Parts** - For EACH strand in your HyperDrive, you will need one of each of the items listed below. Jesse P and I used 5 in the gates we've created so far, including the one at Edgewater. You can increase it to 6 to supersize the effect. Or, you can reduce it, but be aware that the effect will loose some "wow" factor if you do. With 5 strips, it used 2 1/2 5 meter rolls of LEDs. There is also an experimental way of reducing the number of NANOs in your design (see "Reduce Your NANO Load" below).
- Arduino Nano
- WS2812B LED Strips (length and quantity depends on the size of your gate)
- Resistor (220-470 ohm) - Optional but suggested
- Various Wire
- Heatshrink Tubing to cover and protect the electronics and connections

WS2812b Strips can be found here: https://www.amazon.com/ALITOVE-Addressable-Programmable-Waterproof-Raspberry/dp/B07FVR6W71
**OR** if you have some time to wait, they can be found on https://www.aliexpress.com/ - Use the search "WS2812b 5v IP30 5m 60led/m" and you should find them for about $14 per 5m roll (about half the price of Amazon).

The connections are fairly simple and can be repeated for as many LED strands you want in your gate.
# ![Schematic](media/HyperDriveCircuit.jpg)

## IMPORTANT - Power Supply Selection
You will need a 5v power supply for this gate. The type and rating of the power supply you select depends on the **TOTAL** number of LEDs that will be in your gate. As a rule of thumb, you will need about 18W of power at 5v for every meter of LEDs you are running, which is about 60 LEDs. The 8 foot gate at Flite Test used nearly 900 LEDs, which comes out to a 270 watt power supply. We settled on a lower 150W supply like this: https://www.amazon.com/SHNITPWR-Converter-Adapter-Transformer-WS2812B/dp/B07TZ2TRRB
**BUT**, if you plan on doing crazy stuff with your gate like putting other patterns or expanding on the included programming, you may want to opt for the full 300W power supply like this one: https://www.amazon.com/Tanbaby-Universal-Regulated-Switching-Converter/dp/B017YEOAPA

# Programming
Included is a very simple code that will be uploaded to each Nano/LED Strip you have to create the feeling of "Hitting the HyperDrive" and "Flying Through a Starfield". It creates a "star" 7 LEDs long (**LEAD_LEDS**), that fade from the first to the last, traveling at speeds varying between **MIN_STAR_SPEED** and **MAX_STAR_SPEED** down the length of the strand. There can be multiple stars traveling on each strand, controlled by **STARS_PER_STRAND**, that will overtake others if they are traveling faster.
If you encounter issues on programming your NANO boards, please refer to my other gate project on GitHub for more details. https://github.com/Teknoid303/BBTRaceGateProject#firmware

**Number of LEDs** - When installing the LEDs on your HyperDrive, the number of LEDs may differ from those we used on the one at Flite Test, so be sure and count your LEDs and change the following line as needed:

#define NUM_LEDS         147

**Brightness** - Your hyperdrive may be in a dark room, which will require the dimming of the LEDs so that they don't become blinding to the FPV camera. Reduce the number below to your liking. The number runs from 0-255, with 255 being the brightest. 63 is 1/4 brightness, 127 is 1/2, and 191 is 3/4.

#define INIT_BRIGHTNESS   255

# Reduce Your NANO Load 
You **can** reduce the number of NANOs you will need by "looping" three of the strands together in one sequence. At 8 feet, and a total of 441 LEDs, this is the largest number of LEDs that the NANO's dynamic memory will handle gracefully. You will need to add 18-20 feet of shielded wire to your build because you will be sending a data signal a good distance over the wire and it gets very noisy and glitchy at that distance.
- Connect power to your LED strips as normal, but wait on connecting the data line.
- Connect your Arduino NANO to power and the first data connection of your strand.
- At the opposite end of the first strand, connect your shielded wire to the data line, while connecting the shield to the ground. 
- Route the wire back to the opposite end of the gate (the NANO end) and connect the center wire to the data line of the next strand and the shield to ground.
- Repeat the same thing on the 3rd strip.
- Change your NUM_LEDS to the correct number (in the 8 ft case, 441)
- Recompile and load it up.
If you have any issues with this approach, please contact me immediately. I have not experimented at this length of signal line before and it may need some "help" to make the transit.

# Expansion
My original version of this code was much larger and more complicated than this code. It allowed for forward and reversed travel of the stars, along with speed changes via a rotary encoder. It also had single color modes and all sorts of other features... BUT, it would not fit on a simple NANO and required a larger memory than most simple boards could handle. 
For a time-limited project inside the shop at Flite Test, we decided to pull the code down to basics and go with sure-fire version that anyone could load up and run first time.
I plan on expanding this code in a future branch/project that will contain all the features of the original code on a more expandable platform. 

# Recognition
The first known implementation of this design was done by rudiroeller (Martin R) on Instagram. Follow him at https://www.instagram.com/rudiroeller. Therefore, this design is often known as "Rudi's Hyper Drive".
