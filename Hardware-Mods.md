- [Speaker](#speaker)
- [Eject/Select Button](#ejectselect-button)
- [LCD Display](#lcd-display)
- [OLED Display](#oled-display)
- [Rotary Encoder](#rotary-encoder)

## Board Pin Layout
![Board Pin Layout](assets/pinout.png)

## Speaker

A speaker can be attached to the Gotek to sound whenever the floppy
drive heads are stepped. A piezo sounder can be connected directly
between jumper JB and Ground, marked respectively as SPEAKER and GND
in the picture below.

![Piezo speaker](assets/piezo.png)

If you want to connect a magnetic speaker instead, you must buffer via
an NPN transistor. If you don't know what this means just be sure to
use a piezo sounder, easily found on Ebay, and connect it directly as
shown above.

## Eject/Select Button

FlashFloppy supports a third button in addition to the basic up/down
controls. This should be a standard momentary microswitch, connected
to the header pins JA ([Rotary Encoder](#rotary-encoder)).

The button's effect depends on the current state of operation:
- When an image is loaded, the button will immediately eject it
- When selecting an image, the button will immediately confirm the
  currently-selected image

## LCD Display

As an alternative to the Gotek 7-segment display, FlashFloppy supports
the ubiquitous 1602 LCD with I2C backpack board. These are available
from many Ebay sellers. The connections should be made just as for HxC
Gotek firmware, including pullup resistors (if required - see below).

You can locate SCL, SDA, and GND on your Gotek PCB as below. These
connect to the corresponding header pins on your LCD I2C backpack
module.

![LCD data/clock interface](assets/lcd-backpack.png)

VCC (aka 5V) can be found in various places, including just behind the
floppy power connector.

The SCL and SDA lines must be connected to VCC ("pulled up" to VCC)
via 4.7k resistors.  Note that many I2C boards have the pullup
resistors on board and in this case you do not need to attach your own
external pullups. You can confirm this by checking the resistance
between SDA/SCL and VCC. If it is less than 10k you do not need to add
pullups.

If you do require the pullup resistors, these can be soldered to the
backside of the Gotek PCB between VCC and each of SDA and
SCL. Alternatively can be soldered to the back of the I2C module
header as below.

![LCD Pullup Resistors](assets/pullups.jpg)

## OLED Display

Another alternative to the Gotek 7-segment display is a 0.91" 128x32
display, as sold for Arduino projects by many Ebay sellers. You will
require a display with I2C interface: you should see it has a 4-pin
header marked GND, VCC, SCL, SDA.

These displays can simply connect to the 7-segment display's header,
reusing the existing jumper wires, as in the pictires below.

![OLED Display Front](assets/OLED.png)

## Rotary Encoder

As an alternative to using the up/down buttons you can instead connect
a rotary encoder. The picture below shows how to connect it, either
directly or via a PCB module (eg KY040).

If connecting directly note that by convention GND is always the
middle pin in the row of three. If there is a further row of
two pins then these are connected to an internal push switch: you can
wire these pins to jumper JA to use the switch as an
[eject/select button](#ejectselect-button).

PCB Rotary Encoder Connection
![Rotary Encoder Connection](assets/rotsel-pcb.png)

Direct Rotary Encoder Connection
![Rotary Encoder Connection](assets/rotsel-direct.png)

Rotating the dial should now have the same effect as pushing the
buttons: anti-clockwise for down, and clockwise for up.

Troubleshooting:
- Directional controls are inverted: swap the A and B (aka CLK, DT) wires.
- PCB modules only: Both directions move up (or down):
  - Connect + to 3.3V (marked in picture above); or
  - Remove pull-up resistors from the back of the PCB; or
  - Remove the encoder from the PCB and solder wires directly.
