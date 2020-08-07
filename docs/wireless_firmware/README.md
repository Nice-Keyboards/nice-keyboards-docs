# Wireless Keyboard Firmware

Firmware is an extremely important part of a keyboard. Custom wireless keyboards are still in infancy, so firmwares (while very much usable!) are still heavily being worked on. You may be wondering "why isn't it supported in QMK?". You can read why [here](/nice!nano/faq?id=qmk-firmware-support).


## Options

- ### [BlueMicro](/wireless_firmware/bluemicro) - Recommended
  - BlueMicro is an easy to set up firmware for nRF52 chips utilizing Arduino
  - Pros:
    - Easy to set up
    - Good wireless performance
  - Cons:
    - No USB support
- ### [ZMK](/wireless_firmware/zmk) - New and shiny!
  - ZMK is an extremely promising firmware with a wireless first approach and permissive licensing
  - Pros:
    - Well designed board system leveraging Zephyr RTOS
    - Supports much more than just the nRF52
    - USB support
  - Cons
    - Core functionality is still evolving and incomplete
- ### [QMK Forks](/wireless_firmware/qmk_forks) - Experimental
  - QMK forks exist that let you use QMK with nRF52 chips (the nice!nano is one)
  - Pros:
    - It's QMK!
  - Cons:
    - Not all features are tested
    - Forks lag behind the main QMK repository substantially
    - It's a bit finnicky to set up
    - Legality is in question
