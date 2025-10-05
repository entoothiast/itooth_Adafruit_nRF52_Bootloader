# Bootloader for itooth pogo84

This creates a bootloader for the pogo84 which is lacking LEDs and bootbutton.

The bootloader may be found in:

```
https://github.com/entoothiast/itooth_Adafruit_nRF52_Bootloader/actions

--> Actions
  --> build (pca10059_pogo84)
    --> download `pca10059_pogo84.zip`
      --> extract `pca10059_pogo84_bootloader-0.9.2-34-gdb0cc44_s140_6.1.1.hex`
```

Differences between `pca10059` and `pca10059-pogo84`:

| | `pca10059` | `pca10059-pogo84` |
| - | - | - |
| USB volume label | `NRF52BOOT` | `NRF52-pogo84` |
| Volume `NRF52BOOT`, File `INFO_UF2.TXT` | `Model: Nordic nRF52840 Dongle` | `Model: Nordic nRF52840 Dongle pogo84` |
| Volume `CIRCUITPY`, File `boot_out.txt` | `Board ID:pca10059` | `Board ID:pca10059` |

## Disabling the buttons

src/boards/pca10059_pogo84/board.h

```C
/*------------------------------------------------------------------*/
/* BUTTON
 *------------------------------------------------------------------*/
#define BUTTONS_NUMBER  2

#define BUTTON_1       _PINNUM(1, 6)
#define BUTTON_2       _PINNUM(1, 10)
#define BUTTON_PULL    NRF_GPIO_PIN_PULLUP
```

src/boards/boards.h

```C
#ifndef BUTTON_DFU
#define BUTTON_DFU      BUTTON_1
#endif

#ifndef BUTTON_FRESET
#define BUTTON_FRESET   BUTTON_2
#endif
```

Strategy: Search source for `BUTTON_DFU` and `BUTTON_FRESET` and remove the corresponding code.
