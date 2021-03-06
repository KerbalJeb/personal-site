---
title: "Reflow Oven PCB"
collection: projects
header:
    teaser: /assets/images/reflow-pcb-whole.jpg
pcb_fixes_gallery:
    - url: /assets/images/reflow-pcb-fix-res.jpg
      image_path: /assets/images/reflow-pcb-fix-res.jpg
      title: "Adding a Pulldown resistor to the reset pin"
    - url: /assets/images/reflow-pcb-fix-rect.jpg
      image_path: /assets/images/reflow-pcb-fix-rect.jpg
      title: "Soldering the rectifier on upside down"

---

I'm working on converting a toaster oven into a reflow oven to make using SMD part easier. Mostly this requires a custom temperature controller board to allow for the correct temperature profiles. To this end I have designed a temperature control board based around the STM32F042. I chose this chip because it features crystal less USB, so I can relatively easily configure it as a virtual USB COM port to set new temperature profiles. A solid state relay is used to turn on and off the heater elements so they can be switched at higher speeds then a mechanical relay would allow. The board also features a small onboard transformer/rectifier circuit so that is it can be powered directly from mains power, without the need for a separate power supply. The temperature is measured through the use of a thermocouple and a MAX31855 amplifier. The last feature I added is the ability to connect to a small I2C OLED display and some buttons to add a basic UI to to oven.

![Finished PCB](/assets/images/reflow-pcb-whole.jpg)

Designing the board in Altium was relatively straight forward, it mostly consisted of adding the recommended bypass capacitors for the microcontroller, the crystal-less simplified the layout of the mcu significantly. I added some ferrite beads and a small filter cap to the thermocouple input after looking at a breakout board for the MAX31855, this should help reduce high frequency that might be picked on on the thermocouple input. This is important as the thermocouple voltages are quite small (10s of mV), so they are quite susceptible to noise. Wiring up the USB connector was quite straight forward, since the trace are very short and I will only be using Full-Speed USB, I did not worry about impedance matching the traces (impedance matching is recommended in the standard). I did add a TVS diode to the USB data lines as recommended by ST, this is to help protect the GPIO pins from static discharges on the USB port. Normally pull-up/down resistors are required on the D+ and D- lines to indicate if the connection is to a device or host; however, this is not required as the mcu does this internally.  The last consideration with USB was I wanted to use a USB-C connector as I think they are generally a bit nicer than the other options. This require a little bit of extra work as USB-C connectors also support USB 3.0 and 3.1, these protocols are much faster but have extra data lines so we need to indicate that we will only be using the USB 2 protocol. This is done by pulling down both the CC1 and CC2 pins and connecting the top and bottom D+ and D-. This is because USB C connectors are more or less symmetrical on the top and bottom to allow them to be plugged in in both orientations, in USB 3.1 both the top and bottom connectors are used to double the data transfer rate. Since we will just be using USB 2, we need to connect the top and bottom connectors together for USB to function correctly.


![PCB Layout](/assets/images/reflow-pcb-layout.png)

Hand soldering the board was not too bad, despite it being mostly SMD. A bit of flux and solder wick made soldering the MCU and USB connector straight forward, despite their relatively fine pitch.  Hand soldering 0603 components is defiantly the lower limit of what I can hand solder, but they are still quite manageable.

![USB C Connector soldered](/assets/images/reflow-pcb-usb-c.jpg)

Soon after assembling the board I realised that the footprint for my rectifier was mirrored, this had the effect of shorting out my PSU when I attempted to power it with +5V (bypassing the transformer), fortunately the current was limited so no damage was done. I 'fixed' this by soldering the rectifier in upside down (bending the leads to make it work). My goal here was just to get a working version of the board, so I could fix all the issues in the next revision. The next issue I ran into was forgetting to add a pull down resistor to reset pin, obviously this caused some problems when trying to program the MCU. Since the reset and GND pins are both broken out on the SWD header, so I just soldered a THT resistor between them. The last issue I found was somehow I hadn't connected the chip select pin on the MAX31855. This was fixed with a bit of enamel wire and some careful soldering.

{% include gallery id="pcb_fixes_gallery" %}

Soon after assembling the board I realised that the footprint for my rectifier was mirrored, this had the effect of shorting out my PSU when I attempted to power it with +5V (bypassing the transformer), fortunately the current was limited so no damage was done. I 'fixed' this by soldering the rectifier in upside down (bending the leads to make it work). My goal here was just to get a working version of the board, so I could fix all the issues in the next revision. The next issue I ran into was forgetting to add a pull down resistor to reset pin, obviously this caused some problems when trying to program the MCU. Since the reset and GND pins are both broken out on the SWD header, so I just soldered a THT resistor between them. The last issue I found was somehow I hadn't connected the chip select pin on the MAX31855. This was fixed with a bit of enamel wire and some careful soldering.

![Testing the PCB](/assets/images/reflow-pcb-test.jpg)