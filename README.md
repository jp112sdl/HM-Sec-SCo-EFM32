# HM-Sec-SCo-EFM32
Homebrew firmware for the HM-Sec-SCo, that can also be used with an HmIP-SWDO and HmIP-SWDO-I

- [x] EFM32G200F64 Arduino IDE Integration
  - [x] SPI communication with CC1101 module
  - [x] get AlarmClock / Timer working
  - [x] use internal EEPROM (emulated)
  - [x] use external EEPROM (if M24M01 is mounted on pcb)
  - [x] internal vcc measurement
  - [x] external battery measurement
  - [x] use address/serial from unique chip id
  - [x] Sleep-Mode
- [x] Unlock SWD interface
- [x] Upload code with ST-Link V2 using [OpenOCD](https://openocd.org)

<hr/>

HM-Sec-SCo PRG1 Pinout

![pinout](hm-sec-sco-pcb_pinout.png)

<hr/>

### Software part
- **1.)** Install Arduino IDE 1.8.5 or higher
- **2.)** [Add third party board support](https://support.arduino.cc/hc/en-us/articles/360016466340-Add-or-remove-third-party-boards-in-Boards-Manager) from `https://raw.githubusercontent.com/jp112sdl/ARDUINO_EFM32/master/package/package_ARDUINO_EFM32_index.json`
- **3.)** Search for "efm32" and install the board
- **4.)** Download AskSinPP [`dev_efm32`](https://github.com/jp112sdl/AskSinPP/tree/dev_efm32) Branch (Code->Download ZIP) and extract it to the Arduino libraries directory

### Hardware part
- **1.)** Connect ST-LinkV2 to the PCB PRG1 pads using 4 wires (GND, 3.3V, SWCL, SWDIO)
- **2.)** Unlock SWD access
  - start OpenOCD with `openocd -f interface/stlink-dap.cfg -f target/efm32.cfg`
  - connect to openocd using `telnet localhost 4444`
  - unlock with 
 ```
efm32.dap apreg 0 0x4 0xcfacc118
efm32.dap apreg 0 0x0 1
efm32.dap apreg 0 0x8
sleep 1000
efm32.dap apreg 0 0x0 2
reset_config none
reset init
```
- **3.)** _for debugging it is helpful to connect a FTDI interface to the TX pin to read serial debug messages_
- **4.)** Upload code with `/usr/local/bin/openocd -f interface/stlink-dap.cfg -f target/efm32.cfg -c "program /path/to/.elf verify reset exit"`

### :warning: ST-Link V2 Firmware (Bug?)
After upgrading the firmware of my ST-Link V2 from V2J**29S7** to V2J**32S7** (or newer) it was no longer possible for me to unlock debug access!<br/>
I did not find the firmware V2J**29S7** online, but it works with V2J**28S6**, too.<br/>
So I added this firmware update to the repository ([stsw-link007-V2J28S6.zip](https://github.com/jp112sdl/HM-Sec-SCo-EFM32/raw/master/stsw-link007-V2J28S6.zip)).
