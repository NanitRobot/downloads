

Bootloader recording requires access to the `ISP` bus via any third-party programmer.

```zsh
  avrdude -c usbtiny -p m2560 -U efuse:w:0xFD:m -U hfuse:w:0xD8:m -U lfuse:w:0xFF:m -U flash:w:nanite_v3.1.with_bootloader.hex:i - b 152000
```

This example uses `usbtiny`. Along with programming the bootloader, the necessary fuses are installed



Fusebit table
-------------

|   Fuse  | Value|
|:-------:|:----:|
| H-fuse  | 0xD8 |
| L-fuse  | 0xFF |
| E-fuse  | 0xFD |

Supported programmers
---------------------
You can use any programmer that allows you to overwrite the bootlotler

List of supported programmers by your bootloader recording utility you need to enter a command

```zsh
  avrdude -c what
```