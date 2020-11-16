# Troubleshooting

Troubleshooting your nice!nano often falls on to the firmware of choice, but a few directly hardware related items can be addressed.

## My nice!nano seems to be acting up and I want to re-flash the bootloader

### I can still get into the existing bootloader over USB

In this case you can most likely re-flash the bootloader using [`adafruit-nrfutil`](https://github.com/adafruit/Adafruit_nRF52_nrfutil). Here are the steps you'll want to follow:

1. Follow the installation section [here](https://github.com/adafruit/Adafruit_nRF52_nrfutil#installation). Most likely you'll just need to run `pip3 install --user adafruit-nrfutil`.
2. Download the [DFU pkg of the nice!nano bootloader](//docs.nicekeyboards.com/assets/nice_nano_bootloader-_s140_6.1.1.zip).
3. Connect your nice!nano and put it into the bootloader using a double-tap reset.
4. Run the following command in your terminal:

```shell
adafruit-nrfutil --verbose dfu serial --package nice_nano_bootloader-_s140_6.1.1.zip -p SERIALPORT -b 115200 --singlebank --touch 1200
```

However, replace `SERIALPORT` with your respective serial port name on your OS.

- On Windows it will be in the format of `COM8`, but the number 8 will depend on what it is in your device manager under serial.
- On MacOS and Linux it will look something like `/dev/ttyS0`, but you'll of course need to double check the exact path name.

After this runs, you should have your bootloader all re-flashed and fresh.

### I can't get into the bootloader at all anymore

If you can't get into the bootloader anymore, this will mean you'll need a device programmer. You can select one of the two below and use the steps listed.

#### [J-Link (~\$30)](https://www.amazon.com/Segger-J-Link-EDU-mini-Debugger/dp/B0758XRMTF)

1. Plug in your nice!nano over USB
2. Connect these 4 pins to the nice!nano (use the [pinout](/docs/nice!nano/pinout_schematic) as reference)
   1. VCC/VTref will connect to the VCC pin on the nice!nano
   2. GND will connect to any of the GND pins on the nice!nano
   3. SWDIO will connect to the SWD pin on the back of the nice!nano
   4. SWCLK will connect to the SWC pin on the back of the nice!nano
3. Download the [bootloader hex](//docs.nicekeyboards.com/assets/nicenano_bootloader_v1.hex)
4. Download [`nrfjprog`](https://www.nordicsemi.com/Software-and-tools/Development-Tools/nRF-Command-Line-Tools/Download#infotabs)
5. Run this command in your terminal 

```shell
nrfjprog -f NRF52 --program nicenano_bootloader_v1.hex --chiperase
```

#### [ST-Link v2 (~\$4)](https://www.aliexpress.com/wholesale?trafficChannel=main&d=y&CatId=0&SearchText=st+link+v2&ltype=wholesale&SortType=total_tranpro_desc&groupsort=1&page=1)

1. Plug in your nice!nano over USB
2. Connect these 2 pins to the nice!nano (use the [pinout](/docs/nice!nano/pinout_schematic) as reference)
   1. SWDIO will connect to the SWD pin on the back of the nice!nano
   2. SWCLK will connect to the SWC pin on the back of the nice!nano
3. Download the [bootloader hex](//docs.nicekeyboards.com/assets/nicenano_bootloader_v1.hex)
4. Download [`openocd`](https://github.com/xpack-dev-tools/openocd-xpack/releases)
5. Run this command in your terminal

```shell
openocd -f interface/stlink.cfg -f target/nrf52.cfg -c "gdb_flash_program enable" -c "gdb_breakpoint_override hard" -c "init" -c "reset halt" -c "flash write_image erase ./nicenano_bootloader_v1.hex"
```

## My nice!nano won't connect to my host device over BLE

Unfortunately there's likely not much you can do from a hardware perspective if you're running into this. This will mostly likely come down to two factors: the firmware you're using and how nicely the host BLE stack works with said firmware.

Because there's no simple way for me to offer advice on how to fix this, I would instead ask you to reach out to the respective firmware communities to ask for assistance. In general though, I would first test to see if you can connect to your phone over BLE. This will show whether it's a hardware issue or not. In my experience it's never truly been the nice!nano that has hardware issues, so continued work on the firmware side and OS stack side need to occur.
