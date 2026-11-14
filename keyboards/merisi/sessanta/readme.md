# Merisi Sessanta

![Merisi Sessanta](https://merisi.works)

60% PCB for the Merisi Sessanta: split Backspace and split right Shift options, 1.5u / 1u / 1.5u / 7u / 1.5u / 1u / 1.5u
bottom row. Soldered MX switches, STM32F072RBT6, USB-C on a daughterboard connected by a 4-pin JST cable.

* Keyboard maintainer: Merisi Works
* Hardware supported: Merisi Sessanta PCB
* Hardware availability: [Merisi Works](https://merisi.works)

Make example for this keyboard (after setting up your build environment):

    make merisi/sessanta:default

Flashing example for this keyboard:

    make merisi/sessanta:default:flash

See the [build environment setup](https://docs.qmk.fm/#/getting_started_build_tools) and the
[make instructions](https://docs.qmk.fm/#/getting_started_make_guide) for more information. Brand new
to QMK? Start with our [Complete Newbs Guide](https://docs.qmk.fm/#/newbs).

## Layouts

`LAYOUT_60_ansi_tsangan_split_bs_rshift` has every switch position: split Backspace (the right half is `` ` ``)
and split right Shift (the 1u right half is Fn, `MO(1)`). `LAYOUT_60_ansi_tsangan` is the same board with a 2u
Backspace and a 2.75u right Shift. Both are QMK community layouts.

## Bootloader

Enter the bootloader in 3 ways:

* **Bootmagic reset**: hold down Esc and plug in the keyboard (this also clears the stored settings)
* **Physical reset button**: briefly press the button labelled RESET on the PCB
* **Keycode in layout**: press the key mapped to `QK_BOOT` if it is available

The board then shows up as "STM32 BOOTLOADER" (`0483:df11`). The STM32 bootloader is in ROM, so the
RESET button works whatever firmware is on the chip.
