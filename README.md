# Merisi QMK firmware

Open-source firmware for Merisi keyboards, built on [QMK](https://qmk.fm). Use it as it is with
[VIA](https://usevia.app) or [Vial](https://get.vial.today), or as a starting point for your own QMK keymap.

| Keyboard | Folder | Status |
| --- | --- | --- |
| Merisi Sessanta | [`keyboards/merisi/sessanta`](keyboards/merisi/sessanta) | Tested on hardware |

## Download

Ready-to-flash files are on the [Releases page](../../releases/latest). Pick one:

| File | Use it with |
| --- | --- |
| `merisi_sessanta_via.bin` + `merisi_sessanta_via.json` | **VIA** (recommended): remap keys in the VIA web app |
| `merisi_sessanta_vial.bin` | **Vial**: remap keys in the Vial app, no extra file needed |
| `merisi_sessanta_default.bin` | plain QMK, fixed keymap |

Flashing any of them resets the stored keymap to the default layout.

## Flashing the Merisi Sessanta

1. **Enter the bootloader.** Either press the **RESET** button on the PCB, or hold **Esc** while plugging
   in the cable. The keyboard stops typing and the computer sees a device called "STM32 BOOTLOADER".

   > **Warning:** holding Esc while plugging in also **erases your saved keymap and settings**, even if
   > you then don't flash anything. Back up your layout first (VIA: Save + Load; Vial: File, Save current
   > layout), or use the RESET button, which keeps them until you flash.
2. **Flash the `.bin`**, with one of:
   * [QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases) (macOS / Windows): open the `.bin`, click
     **Flash**.
   * `dfu-util` (any OS):

         dfu-util -a 0 -d 0483:df11 -s 0x08000000:leave -D merisi_sessanta_via.bin

3. The keyboard restarts by itself. If it doesn't, unplug it and plug it back in.

The bootloader is built into the chip, so the RESET button always works, even if a flash goes wrong:
just flash again.

## Using VIA

VIA doesn't know the Sessanta yet, so load its definition once:

1. Open [usevia.app](https://usevia.app) in Chrome or Edge.
2. **Settings**: turn on **Show Design tab**.
3. **Design**: load `merisi_sessanta_via.json`.
4. **Configure**: connect the keyboard and remap. The **Layouts** tab has the split Backspace and split
   right Shift options.

VIA's "Test Matrix" stays blank: QMK keeps raw switch states private unless the firmware is built
insecure. Use VIA's normal key tester, or Vial's matrix tester.

## Using Vial

Open [Vial](https://get.vial.today) (desktop app or web). The layout is built into the firmware, so there
is nothing to load. To use the matrix tester or other locked features, unlock by holding **Esc + Enter**
when Vial asks.

## Merisi Sessanta

* 60% PCB, STM32F072RBT6, USB-C daughterboard on a 4-pin JST cable, RESET button.
* Layouts: split Backspace and split right Shift (the 1u right half is Fn); bottom row
  1.5u / 1u / 1.5u / 7u / 1.5u / 1u / 1.5u. QMK layout names: `LAYOUT_60_ansi_tsangan_split_bs_rshift`,
  `LAYOUT_60_ansi_tsangan`.
* USB id `4D57:5336`, shown as "Sessanta" by "Merisi".
* Default keymap: standard ANSI. Fn (`MO(1)`) is on the right of the split right Shift; layers 1-3 are
  empty for you to fill.

## Building from source

**Plain QMK or VIA** (upstream [QMK](https://github.com/qmk/qmk_firmware), tested with 0.34.8):

    cp -R keyboards/merisi/sessanta <qmk_firmware>/keyboards/merisi/
    qmk compile -kb merisi/sessanta -km default     # or -km via, or your own keymap

**Vial** ([Vial-QMK](https://github.com/vial-kb/vial-qmk), tested at `dd43959`):

    cp -R keyboards/merisi/sessanta <vial-qmk>/keyboards/merisi/
    make merisi/sessanta:vial

The release Vial build also applies [`patches/vial-nkro-default.patch`](patches/vial-nkro-default.patch)
to Vial-QMK, so that "Reset settings" in Vial keeps N-key rollover on (the keyboard's default). Without
it the firmware works the same, except that a settings reset turns N-key rollover off.

Toolchain used for the releases: `arm-none-eabi-gcc` 8.5.0.

## License

GPL-2.0-or-later, the same as QMK. See [LICENSE](LICENSE). You may use, change and share this firmware;
if you distribute a modified build, share its source too.
