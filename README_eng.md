Default firmware
================

Here are the firmwares for ```Nanit``` which are installed by default.
If in the process of studying programming you could not independently write the behavior algorithms implemented by us and you want to play with the modes written for you by the creators and authors of ```Nanit```, you can restore them using the functions of the Arduino IDE or using special utilities

- [Discovery](./nanite_v3.1.ino.hex)
- [Smart Home](./ud_v3.1.ino.hex)

Arduino IDE
-----------

#### Arduino 1.8

         In the process of development

#### Arduino (new)

         In the process of development

No IDE
-------
To restore the default firmware without using the Arduino IDE, you must have the ```avrdude``` application installed on your PC and all drivers and dependencies configured.

__ATTENTION this command is only valid for ```LinuxOS```__
```zsh
avrdude -c wiring -p m2560 -U flash:w:./NanitInfo.ino.hex:i -P /dev/ttyUSB0
```
### Explanation
We run `avrdude` using the built-in programmer (`wiring`) for the __ATmega2560__ microcontroller to write the contents of the file [NanitInfo.ino.hex](./NanitInfo.ino.hex), which contains the executable code in IntelHex format, to the flash memory: `i` through port `/dev/ttyUSB0`

Clearing the EEPROM
===================

Note Clear memory erases all presets.
We are not responsible for the performance of some modes of ```Nanit Discovery```, and warranty service restrictions for ```Nanit``` ```Discovery``` and ```Smart Home``` may apply.

Instructions for service technicians

We connect the main unit to the PC using a cable and execute the command in the terminal or in the command line emulator

```zsh
avrdude -c wiring -p m2560 -b 152000 -U eeprom:w:CLEAR_EEPROM.hex:i
```
### Explanation
We run `avrdude` using the built-in programmer (`wiring`) for the __ATmega2560__ microcontroller at a speed of `152000` baud to write the contents of the file [CLEAR_EEPROM.hex](./CLEAR_EEPROM.hex) into the EEPROM, which contains data for the non-volatile memory in IntelHex `:i` format


Bootloader entry
================

__CAUTION__ do not attempt to flash the bootloader firmware via the on-board programmer. Bootloader recording requires access to the ```ISP``` bus via any third-party programmer.

![ISP](https://raw.githubusercontent.com/NanitRobot/NanitLib/main/pic/ISP_Nanit.png)

One of the files is required to write the bootloader firmware

- [Discovery with bootloader](./nanite_v3.1.with_bootloader.hex)
- [NanitInfo with bootloader](./NanitInfo.ino.with_bootloader.hex)


To write the program to the ```Nanit``` board, you need to use the `avrdude` utility.

```zsh
  avrdude -c usbtiny -p m2560 -Ulock:w:0x3F:m -U efuse:w:0xFD:m -U hfuse:w:0xD8:m -U lfuse:w:0xFF:m -U flash:w:NanitInfo.ino.with_bootloader.hex:i - b 152000
```

  This example uses `usbtiny`. Necessary fuses are installed along with bootloader programming


|   Fuse  | Value|
|:-------:|:----:|
| lock    | 0x3F |
| hfuse   | 0xD8 |
| lfuse   | 0xFF |
| efuse   | 0xFD |

Supported programmers
---------------------

To find out the supported programmers by your bootloader recording utility, you need to enter the command

```zsh
  avrdude -c what
```
