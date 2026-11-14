# Merisi QMK firmware

This repository has the firmware for Merisi keyboards. The firmware uses [QMK](https://qmk.fm). You can use it
with [VIA](https://usevia.app) or [Vial](https://get.vial.today), or you can use it as the base for your own QMK keymap.

| Keyboard | Folder | Status |
| --- | --- | --- |
| Merisi Sessanta | [`keyboards/merisi/sessanta`](keyboards/merisi/sessanta) | Tested on hardware |

## Download

The files to flash are on the [Releases page](../../releases/latest). Select one of these options:

| File | Use |
| --- | --- |
| `merisi_sessanta_via.bin` and `merisi_sessanta_via.json` | **VIA (recommended).** Change the keymap in the VIA web app. |
| `merisi_sessanta_vial.bin` | **Vial.** Change the keymap in the Vial app. You do not need an extra file. |
| `merisi_sessanta_default.bin` | Plain QMK with a fixed keymap. |

When you flash a file, the keyboard erases its saved keymap and uses the default layout.

## Flash the Merisi Sessanta

1. Put the keyboard in bootloader mode. Push the **RESET** button on the PCB, or hold **Esc** while you connect the cable.
   The keyboard stops typing. The computer then shows a device with the name "STM32 BOOTLOADER".

   > **Warning:** When you hold Esc while you connect the cable, the keyboard erases its saved keymap and settings.
   > This occurs even if you do not flash a file. Before you use Esc, save your layout. In VIA, use the "Save + Load" tab.
   > In Vial, select File, then "Save current layout". The RESET button does not erase the settings.

2. Flash the `.bin` file with one of these tools:
   * [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases) (macOS and Windows). Open the `.bin` file, then click **Flash**.
   * `dfu-util` (all operating systems):

         dfu-util -a 0 -d 0483:df11 -s 0x08000000:leave -D merisi_sessanta_via.bin

3. The keyboard starts again automatically. If it does not start, disconnect the cable and connect it again.

The bootloader is in the chip. Thus the RESET button always operates, also after a flash that failed.
If a flash fails, push RESET and flash again.

## Use VIA

VIA does not have the Sessanta in its list. Load the definition file one time:

1. Open [usevia.app](https://usevia.app) in Chrome or Edge.
2. In **Settings**, turn on "Show Design tab".
3. In **Design**, load `merisi_sessanta_via.json`.
4. In **Configure**, connect the keyboard and change the keymap.

The **Layouts** tab has the options for split Backspace and split right Shift.

The "Test Matrix" function in VIA shows no keys. QMK does not send the switch states to VIA, because other
programs could read the keystrokes. To test the keys, use the key tester in VIA or the matrix tester in Vial.

## Use Vial

Open [Vial](https://get.vial.today) (desktop app or web). The layout is in the firmware, so you do not load a file.
Some functions are locked, for example the matrix tester. To unlock them, hold **Esc** and **Enter** when Vial tells you.

## Merisi Sessanta

* 60% PCB with an STM32F072RBT6 microcontroller and a RESET button.
* A 4-pin JST cable connects the PCB to a USB-C daughterboard.
* Layout options: split Backspace and split right Shift. The 1u key at the right of the split right Shift is Fn.
* Bottom row: 1.5u, 1u, 1.5u, 7u, 1.5u, 1u, 1.5u.
* QMK layout names: `LAYOUT_60_ansi_tsangan_split_bs_rshift` and `LAYOUT_60_ansi_tsangan`.
* USB ID `4D57:5336`. The computer shows the keyboard as "Sessanta" by "Merisi".
* The default keymap is standard ANSI. Fn (`MO(1)`) selects layer 1. Layers 1 to 3 are empty, so you can add your own keys.

## Build from source

To build plain QMK or VIA firmware, use upstream [QMK](https://github.com/qmk/qmk_firmware). We tested version 0.34.8.

    cp -R keyboards/merisi/sessanta <qmk_firmware>/keyboards/merisi/
    qmk compile -kb merisi/sessanta -km default     # or -km via, or your own keymap

To build Vial firmware, use [Vial-QMK](https://github.com/vial-kb/vial-qmk). We tested commit `dd43959`.

    cp -R keyboards/merisi/sessanta <vial-qmk>/keyboards/merisi/
    make merisi/sessanta:vial

The Vial release also uses [`patches/vial-nkro-default.patch`](patches/vial-nkro-default.patch) on Vial-QMK.
With this patch, "Reset settings" in Vial keeps N-key rollover on, which is the default for this keyboard.
Without the patch, the firmware operates the same, but a settings reset sets N-key rollover to off.

We built the releases with `arm-none-eabi-gcc` 8.5.0.

## License

This firmware has the GPL-2.0-or-later license, the same as QMK. Refer to [LICENSE](LICENSE).
You can use, change, and share this firmware. If you share a changed build, you must also share its source code.
