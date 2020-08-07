# FAQ

### Will the nice!nano work on x keyboard?

Probably. Almost every Pro Micro based keyboard should work with the nice!nano. Limitations would be around height of the board (fitting a battery underneath will make the entire module + battery 6mm tall when hotswapped for example) and running at 3.3V rather than 5V, which shouldn't be much of an issue. Tested on the Lily58, Semaphore, and Kyria so far.

!> The nice!nano will *NOT* work with the Gherkin unless you don't connect the RAW pin to the board.

### How is the nice!nano powered/how do the split boards power each other?

They don't charge each other, each has an individual Li-Po battery connected to it via 2 extra pins at the top of the board (called B+ and B-).

### How do you charge the nice!nano?

The nice!nano has a Li-Po charger built in that uses the USB-C port to charge the Li-Po at a rate of 100mA.

### How long does the nice!nano last on battery?

This is highly dependent on the battery size and features of the keyboard. With no extra OLEDs or LEDs, my Lily58 lasts a couple weeks on a 110mAh battery. It charges back up in an hour and can be used while charging.

### Does the nice!nano work over USB?

Yes, but not every firmware supports it.

### QMK firmware support?

This is complicated. Nordic's nRF52 line has some licensing issues with its SDK making it not possible to be upstreamed to the main QMK repo. There are some QMK forks such as sekigon's, but the legality is questionable at best. At the same time the BlueMicro firmware (https://github.com/jpconstantineau/BlueMicro_BLE) is available and promising in my opinion. Take a look and contribute! It works with the nice!nano.

### Can I get more information on nRF52840 hardware?

Joric's nRFmicro wiki is an amazing resource to get some basic and advanced information on the nRF52 line in terms of keyboards: https://github.com/joric/nrfmicro/wiki

### How is this different from the nRFMicro or BlueMicro?

The nRFmicro is extremely similar to the nice!nano. The main difference is depending on the version of the nRFMicro, the power system would be slightly different from the nice!nano. From a usability standpoint, very little is different. The nice!nano exposes more pins and is thinner than older versions of the nRFMicro. The biggest difference is that the nice!nano is assembly ready, so they can be mass produced more easily than the nRFMicro (hence the GB). The BlueMicro is basically the same story except for the nRF52832 versions don't support USB.

### Do you still need a TRRS jack?

No, there's a connection via BLE between the two boards. The master reports back the keystrokes of both sides.
