VoodooPS2
=========

适用于同方部分机型的 VoodooPS2 键盘相关驱动，修复兼容问题，支持所有 Fn 功能键。

Custom VoodooPS2 kernel extension series for **Tongfang** ODM laptops.

## Features

- Fix Incompatibility.
- Full Fn Key Functionality.

## Fn Keys

| Fn + Fx  | Function                             | Note                   |
| -------- | ------------------------------------ | ---------------------- |
| F1       | Sleep                                | -                      |
| F2       | Lock LGUI Key                        | -                      |
| F3       | Switch Screen Mirroring/Extended     | Open display settings. |
| F4       | Toggle WiFi                          | -                      |
| F5       | Toggle Touchpad                      | -                      |
| F6, F7   | Increase/Decrease Keyboard Backlight | -                      |
| F8 - F10 | Adjust Volume                        | -                      |
| F10, F11 | Adjust Screen Backlight              | -                      |

## Install

1. Copy `VoodooPS2Controller.kext` into `kexts/Other`；
2. Copy `SSDT-FN.aml` into `ACPI/patched`；
3. Patch `clover-patch-config.txt` into DSDT section of `config.plist`；
4. Install `TongfangFnDaemon` with `install_daemon.sh`；
5. Reboot.

## Credits

[hieplpvip/AsusSMC](https://github.com/hieplpvip/AsusSMC)

---

New **VoodooPS2Trackpad** emulates Magic Trackpad II using macOS native driver instead of handling all gestures itself. This enables the use of any from one to three finger gestures defined by Apple including:
* Look up & data detectors
* Secondary click (*with two fingers, in bottom left corner\*, in bottom right corner\**)
* Tap to click
* Scrolling
* Zoom in or out
* Smart zoom
* Rotate
* Swipe between pages
* Swipe between full-screen apps (*only with three fingers*)
* Notification Centre
* Mission Control (*only with three fingers*)
* App Exposé (*only with three fingers*)
* Dragging with or without drag lock (*configured in 'Universal Access' prefpane*)
* Three finger drag (*configured in 'Universal Access' prefpane, may work unreliably\*\**)

It also should support **BetterTouchTool** (not tested).

In addition this kext supports **Force Touch** emulation (*configured in `Info.plist`*):
* **Mode 0** – Force Touch emulation is disabled (*you can also disable it in **System Preferences** without setting the mode*).
* **Mode 1** – Force Touch emulation using a physical button: on touchpads which have the whole surface clickable (the physical button is inside the computer under the bottom of touchpad), the physical button can be remapped to Force Touch. In such mode a tap is a regular click, if **Tap to click** gesture is enabled in **System Preferences**, and a click is a Force Touch. This mode is convenient for people who usually tap on the touchpad, not click.
* **Mode 2** – *'wide tap'*: for Force Touch one needs to increase the area of a finger touching the touchpad\*\*\*. The necessary width can be set in `Info.plist`. 
* **Mode 3** shouldn't be used.

## Credits:
* VoodooPS2Controller etc. – turbo, mackerintel, @RehabMan, nhand42, phb, Chunnan, jape, bumby (see RehabMan's repository).
* Magic Trackpad 2 reverse engineering and implementation – https://github.com/alexandred/VoodooI2C project team.
* VoodooPS2Trackpad integration – @kprinssu.
* Force Touch emulation and finger renumbering algorithm** - @usr-sse2.

\* On my touchpad this gesture was practically impossible to perform with the old VoodooPS2Trackpad. Now it works well.  
\*\* Due to the limitations of PS/2 bus, Synaptics touchpad reports only the number of fingers and coordinates of two of them to the computer. When there are two fingers on the touchpad and third finger is added, a 'jump' may happen, because the coordinates of one of the fingers are replaced with the coordinates of the added finger. Finger renumbering algorithm estimates the distance from old coordinates to new ones in order to hide this 'jump' from the OS and to calculate approximate position of the 'hidden' finger, in assumption that fingers move together in parallel to each other.  
\*\*\* The touchpad reports both finger width (ranged from 4 to 15) and pressure (ranged from 0 to 255), but in practice the measured width is almost always 4, and the reported pressure depends more on actual touch width than on actual pressure.
