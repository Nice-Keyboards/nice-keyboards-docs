# Wireless Keyboard Firmware

Firmware is an extremely important part of a keyboard. Custom wireless keyboards are still in infancy, so firmwares (while very much usable!) are still heavily being worked on. You may be wondering "why isn't it supported in QMK?". You can read why [here](/nice!nano/faq?id=qmk-firmware-support).


## Options

- ### [ZMK](/wireless_firmware/zmk) - Recommended
  - ZMK is an extremely promising firmware with a wireless first approach and permissive licensing
  - Pros:
    - Well designed board system leveraging Zephyr RTOS
    - Best-in-class power usage
    - Extremely easy to set up with no local build environment required
    - Supports much more than just the nRF52 including many ARM wired keyboards
    - USB support
  - Cons
    - Understanding the board system may take some time for those used to other firmwares
- ### [BlueMicro](/wireless_firmware/bluemicro) - Recommended
  - BlueMicro is an easy to set up firmware for nRF52 chips utilizing Arduino
  - Pros:
    - Based on Arduino, which some may be familiar with
    - Reliable wireless connection between halves
  - Cons:
    - No USB support
    - Higher power usage
    - Locked into the nRF52 ecosystem
