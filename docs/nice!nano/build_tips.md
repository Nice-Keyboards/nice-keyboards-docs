# Build Tips

This page is a long list of tips and reminders before you use the nice!nano to build your board.

## Batteries
- ONLY use 3.7v rechargeable lithium batteries with the nice!nano. Connecting non-rechargeable batteries to the board is unsafe.
- When soldering the battery, use the B+ and B- pins at the top of the board (see [pinout](/nice!nano/pinout)). Minimize how long you are holding the soldering iron on the battery. High amounts of heat are dangerous to connect the battery to.
- You can also use RAW and GND pins instead of B+ and B- pins respectively, although this isn't as convenient most likely.

## Socketing
- Socketing the nice!nano is *extremely* recommended. It offers ease of access to the battery, helps you if you need to debug your keyboard, and lets you move the board to another keyboard if ever needed.
- Socketing tips:
  1. First install the socket into the PCB trying to keep it as straight as possible.
  2. Once the sockets are in, place tape over the top of each side.
  3. Poke holes where each socket hole is into the tape
  4. Place down the nice!nano (to assure alignment, make sure the B+ and B- pins are not being put into the socket)
  5. Put diode legs (or MillMax socket pins) into each hole and push all the way down
  6. Solder the legs to the nice!nano (this is where the tape helps, solder wont seep down into the socket and fuse the socket and legs)
  7. Take the nice!nano out by using a pry tool of some sort. Slowly pry back and forth on all sides.
  8. Take away the tape and put the nice!nano back in.
  9. Done!

## Recommended Socket and Battery System
The recommended socket to use is the standard female machine pin sockets. They end up being ~4.75mm tall when installed. This is the perfect height to fit a 301230 battery underneath even if the nice!nano is flipped upside down.

With this setup, the whole socket and battery system is about 6.2mm tall when the nice!nano is flipped upside down and 7.8mm when the nice!nano is right side up.

I sell both items for this setup on my store!
