# Getting Started

This document will guide you through installing your nice!nano and flashing. After following this document, you can move on to the Wireless Firmware page to pick out your software.

## Before you start

Before you install your nice!nano please note these tips/warnings:

 - Do not install sockets or post headers to the B+ or B- pins (top pin on each side)
   - If you need to use these pins with your PCB, RAW and GND are the respective equivalents to B+ and B-
 - The square post headers that come with the nice!nano cannot be used with the machine sockets
   - Use Mill-Max pin legs or diode legs and folow the directions in [installing your nice!nano](#installing-your-nicenano)
 - Only use 3.7V rechargeable lithium batteries with the nice!nano. Connecting non-rechargeable batteries is unsafe
 - If you choose to solder your battery, use the B+ and B- pins. B+ is for the positive, red wire, and the B- pin is for the negative, black wire. Minimize how long you are holding the soldering iron to the battery. High amounts of heat are dangerous to connect the battery to.
 - If you are using a JST connector on the PCB to connect the battery, double or even quadruple check the polarity of the JST connector before plugging it in. Some batteries come with positive on the first pin and some come with negative on the first pin.

## Installing your nice!nano

Installing your nice!nano is almost the same as any other Pro Micro like board. The only difference is related to ignore the B+ and B- pins when adding sockets or headers and **the battery**. It's highly recommended to get your firmware on and functioning before adding the battery.

If you aren't socketing, you probably want to get the firmware up and running before you even attach the square post headers. You'll want to install the firmware, confirm everything is working, and install your square post headers and battery.

If you are socketing, you can socket your nice!nano, install the firmware, confirm everything is working, and finally add the battery.

### Socketing the nice!nano

Socketing the nice!nano is *extremely* recommended. It offers ease of access to the battery, helps you if you need to debug your keyboard, and lets you move the board to another keyboard if ever needed.

For a great guide with pictures check out [40percentclub's guide](http://www.40percent.club/p/socketing-pro-micro.html).

Socketing steps:
  1. First install the socket into the PCB trying to keep it as straight as possible.
  2. Once the sockets are in, place tape over the top of each side.
  3. Poke holes where each socket hole is into the tape
  4. Place down the nice!nano (to assure alignment, **make sure the B+ and B- pins are not being put into the socket**)
  5. Put MillMax pin legs (or diode legs) into each hole and push all the way down
  6. Solder the legs to the nice!nano (this is where the tape helps, solder wont seep down into the socket and fuse the socket and legs)
  7. Take the nice!nano out by using a pry tool of some sort. Slowly pry back and forth on all sides.
  8. Take away the tape and put the nice!nano back in.
  9. Done!

## Flashing, Firmware, and Bootloaders

One of the great things about the nice!nano is how easy it is to flash the device. To jump into the bootloader all you need to do is double tap reset. You can do this by either double tapping your reset button on your keyboard, or you can double tap RST and GND pins on the nice!nano quickly with tweezers.

Once you are into the bootloader, connect your nice!nano via USB to your computer if you haven't already. Your nice!nano should now show up in your OS as a USB storage device named "NICENANO".

Flashing is now as easy as copying a .uf2 firmware file to the storage device. You can do this by copying in the terminal, dragging and dropping it in your file explorer, or however else you copy files to a storage device in your OS.

Now you may be wondering how to get one of these mystical .uf2 files. You get them by building one of the firmwares available. Checkout the [**Wireless Firmware**](/wireless_firmware/) page to get information on how to configure and build a few different types of firmwares along with some recommendations.

The bootloader the nice!nano uses is the Adafruit nRF52 Bootloader. You can read more about its features, updating the bootloader, and using DFU to flash firmware on [its GitHub](https://github.com/adafruit/Adafruit_nRF52_Bootloader).
