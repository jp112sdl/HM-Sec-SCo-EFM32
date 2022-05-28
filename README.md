# HM-Sec-SCo-EFM32
Homebrew firmware for the HM-Sec-SCo, that can also be used with an HmIP-SWDO and HmIP-SWDO-I

- [x] EFM32G200F64 Arduino IDE Integration
  - [x] SPI communication with CC1101 module
  - [x] get AlarmClock / Timer working
  - [x] use internal EEPROM (emulated)
  - [x] use external EEPROM (if M24M01 is mounted on pcb)
  - [x] internal vcc measurement
  - [x] external battery measurement
  - [ ] Sleep-Mode
- [x] Unlock SWD interface
- [x] Upload code with ST-Link V2 using OpenOCD

<hr/>

HM-Sec-SCo PRG Pinout

![pinout](hm-sec-sco-pcb_pinout.png)
