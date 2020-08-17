# QMK Forks
!> QMK forks do work with the nice!nano, but they aren't recommended and have limited support.

## Overview
The QMK forks are recommended only for those familiar with QMK and adding your own QMK board definition.

The most popular QMK fork is [sekigon-gonnoc's nrf52 branch](https://github.com/sekigon-gonnoc/qmk_firmware/tree/nrf52) on his QMK fork.

Use the boards the end with `_ble` in the keyboards directory as reference to construct your own.


> Below is a translated version of https://sekigon-gonnoc.github.io/BLE-Micro-Pro/#/deprecated/README


## Usage (software)

For nrf52 compatible qmk_firmware click [here](https://github.com/sekigon-gonnoc/qmk_firmware/tree/nrf52)

- If you are already using qmk_firmware and want to have it as a separate branch
```
    git remote add sekigon https://github.com/sekigon-gonnoc/qmk_firmware.git
    git fetch sekigon
    git checkout -b nrf52 sekigon/nrf52
```

- If you are already using qmk_firmware and want to put it in a different folder
 ```
    git clone -b nrf52 https://github.com/sekigon-gonnoc/qmk_firmware.git ble_micro_pro
 ```

- When using for the first time
```
    git clone --depth 1 -b nrf52 https://github.com/sekigon-gonnoc/qmk_firmware.git
```

### Build environment
In addition to the environment for pro micro, `arm-none-eabi-gcc` is required. (Confirmed working with Version 7-2017-q4-major)
If everything was installed during the QMK official setup, the environment for arm should be installed at the same time.
If you removed the arm environment and set it up, execute the setup command again to perform an additional installation.

Also, download [nRF5_SDK v15.0.0](https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v15.x.x/) and extract it in a suitable location.

### Firmware creation

#### Option setting

* For Mac, it seems that `MOUSEKEY_ENABLE` in rules.mk must be set to yes for recognition.
* If you specify `ENABLE_STARTUP_ADV_NOLIST` in config.h, advertisement will start automatically at startup.

#### Key map
It is recommended to set the custom code that executes the following functions (on the master side key in case of split type by referring to the sample.

| Function | Description |
|:--|:--|
|advertising_wo_whitelist()|Use when pairing with a new device.
|restart_advertising_id(id)|Try to connect to the device with the specified id. In case of split type, since id=0 is a slave, it is assigned to each device from id=1.
|set_usb_enabled(bool)|Enables/disables sending via USB. It is disabled at startup, so enable it in matrix_init_user or assign it to the keymap.
|set_ble_enabled(bool)|Enables/disables sending via BLE. It is enabled at startup.


### Writing the firmware
It supports writing with SWD and DFU if the boot loader has already been written.
The following describes writing with DFU.

#### Setup (Windows (MSYS2))
Download [nrfutil.exe](https://github.com/NordicSemiconductor/pc-nrfutil/releases) and save it in ~/qmk_util.

#### Setup (Mac, Linux)
Put nrfutil with pip. (python2.7)
    
    pip install nrfutil

#### Creating and writing packages

Please set the nRF SDK location as an environment variable before building

    export NRFSDK15_ROOT=<path to sdk>
  
The first time it takes time to build the library. In case of split type, build both master and slave.

    make <keyboard>/<master or slave>:nrfutil
By executing, you can write the firmware right after build.

> Plug in via USB port, and put your controller into bootloader mode

Press the reset button on the keyboard to power up or launch the bootloader from the command set in the keymap. The bootloader is automatically started when first writing.
If the writing is successful, it will automatically restart and be recognized as a USB keyboard.

[Error occurs when writing](/wireless_firmware/qmk_forks?id=i-get-an-error-that-nrf_delayh-cannot-be-found-when-building)

##### If an error occurs when usb_serial is not found when writing (Mac OS etc.?)
Line 862 of qmk/tmk_core/nrf.mk

    $(NRFUTIL) dfu usb_serial -pkg $(TARGET).zip -p $$USB; \
To

    $(NRFUTIL) dfu usb-serial -pkg $(TARGET).zip -p $$USB; \
Please rewrite

#### (Split type) Master and slave connection
In the case of the split type, please execute the pairing with a personal computer etc. after establishing the connection between the master and slave at the first startup.
For this reason, it is safe to make a USB connection when starting for the first time, open the serial port using terminal software such as TeraTerm, and check the information before connecting.
It is recommended to enable USB transmission of the master and confirm that the input of the slave is reflected before performing pairing with a personal computer.

#### Pairing with a personal computer
When advertising_wo_whitelist() is executed, BLE Micro Pro will start advertising. If you scan from a computer etc., you should be able to confirm the device with the specified keyboard name.

When pairing with the second and subsequent computers, disable Bluetooth on other paired computers and then execute advertising_wo_whitelist().

If you want to connect to the specified paired PC etc., execute restart_advertising_id(id). id is the pairing order. In case of split type, id=0 is assumed to be a slave.

### Create new keyboard firmware
qmk_firmware/keyboard/ble_micro_test is an integrated type, and qmk_firmware/keyboard/ergo42_ble, helix_ble etc. are left-right separated type samples.
#### In case of integrated type
There are two files that need to be edited: ble_micro_test/config.h and ble_micro_test/pro_v1/config.h.

| Parameter | How to change |
|:--|:--|
|MATRIX_ROWS, MATRIX_COLS| As usual |
|THIS_DEVICE_ROWS, THIS_DEVICE_COLS| Set to the same value as MATRIX_ROWS, MATRIX_COLS |
|MATRIX_ROW_PINS, MATRIX_COL_PINS| Specify the pin numbers used for the key matrix |
|IS_LEFT_HAND| Must be true|
|BLE_HID_MAX_INTERVAL| Lowering the communication interval (ms) with the terminal increases power consumption. Default is 90|
|BLE_HID_SLAVE_LATENCY| Lowering the communication parameters with the terminal increases power consumption. Should I make it inversely proportional to HID‗INTERVAL? Default is 4|

#### For split keyboards
Different firmware is required for master and slave. Currently, only the master supports USB connection. There are three files to edit: ergo42_ble/config.h, ergo42_ble/master/config.h and ergo42_ble/slave/config.h.

| Parameter | How to change |
|:--|:--|
|MATRIX_ROWS, MATRIX_COLS| As usual |
|THIS_DEVICE_ROWS, THIS_DEVICE_COLS| Number of columns and rows for each master and slave. Supports up to 8x16 |
|MATRIX_ROW_PINS, MATRIX_COL_PINS| Specify the pin numbers used for the key matrix |
|IS_LEFT_HAND| true for left hand side, false for right hand side|
|BLE_NUS_MAX_INTERVAL| Lowering the communication interval (ms) between left and right increases power consumption. Default is 70|
|BLE_HID_MAX_INTERVAL| Lowering the communication interval (ms) with the terminal increases power consumption. Default is 90|
|BLE_HID_SLAVE_LATENCY| Lowering the communication parameters with the terminal increases power consumption. Should I make it inversely proportional to HID‗INTERVAL? Default is 4|


## FAQ
### I get an error that nrf_delay.h cannot be found when building.
Please make sure that NRDSDK15_ROOT exists and that the downloaded SDK version is correct.

### Hash error (0x0C) appears when writing
Due to a bug in the library used by bootloader (v1.0), it seems that a write error may occur even with a normal binary.

* Rewrite to [latest version of bootloader](https://github.com/sekigon-gonnoc/BLE-Micro-Pro/blob/master/ble_micro_pro_bootloader.zip)
* Change the binary size by commenting out or rewriting the functions in master.c or slave.c

You can write using either method.

Execute the following command to rewrite the bootloader. If you fail to rewrite the bootloader, you may write down, so please do not disconnect the cable.

`nrfutil dfu usb_serial -pkg ble_micro_pro_bootloader.zip -p <port name>`

### An error occurs when usb_serial is not found when writing
Line 862 of qmk/tmk_core/nrf.mk

`$(NRFUTIL) dfu usb_serial -pkg $(TARGET).zip -p $$USB; \`

To

`$(NRFUTIL) dfu usb-serial -pkg $(TARGET).zip -p $$USB; \`

Please rewrite

### My PC or master-slave connection is not working properly
Please erase pairing information from both devices (PC and master, master and slave) and re-pair.

It will be easier to delete and re-pair while checking using the terminal described below.

### I don't know if pairing was successful or if I could erase the information
If you open the terminal of BLE Micro Pro that has been written to the firmware with terminal software such as Tera Terminal, you can check and delete the pairing.

Also, a message is displayed when connecting/disconnecting BLE.

| Command | Description |
|-|-|
|help| Show command list |
|adv| Start device discovery |
|show| Show the number of saved pairings |
|del [id]|Delete id-th pairing|

### Chatter
Try increasing DEBOUNCE in config.h by one.