# Sofle Keyboard

![SofleKeyboard version 1](https://i.imgur.com/S5GTKth.jpeg)

Sofle is 6×4+5 keys column-staggered split keyboard. Based on Lily58, Corne and Helix keyboards.

More details about the keyboard and build guides can be found here: [Sofle Keyboard Build Log and Guide](https://josefadamcik.github.io/SofleKeyboard)

* Keyboard Maintainer: [Josef Adamcik](https://josef-adamcik.cz) [Twitter:@josefadamcik](https://twitter.com/josefadamcik)  
* Hardware Supported: SofleKeyboard PCB, ProMicro  
* Hardware Availability: [PCB & Case Data](https://github.com/josefadamcik/SofleKeyboard)

## Firmware Revisions
- `sofle/rev1` is used for v1, v2, and RGB PCBs (**NOT** RGB PCBs purchased from [Keyhive](https://keyhive.xyz))
- `sofle/keyhive` is used for PCBs purchased from [Keyhive](https://keyhive.xyz/shop/sofle)
- [`keyboards/sofle_choc`](../sofle_choc/) is used for Choc PCBs

# My updates
## Code changes

The following was added to `config.h`:

    #define EE_HANDS
    #define SPLIT_OLED_ENABLE
    #define SPLIT_LAYER_STATE_ENABLE
    #define SPLIT_WPM_ENABLE

This allows for the second OLED screen to receive info from the master side, for things like layers, wpm calcs and turning off the display if the computer goes to sleep.  The `EE_HANDS` combined with the handedness flag in the Flashing section allow for either side to be plugged in and the keys will be mapped as expected.

The following was added to `rules.mk`:

    WPM_ENABLE = yes
    SPLIT_WPM_ENABLE = yes

Which are required for the wpm calculations.

## Flashing

To compile and flash this firmware, run 

    qmk flash -kb sofle/rev1 -km vial -e CONVERT_TO=rp2040_ce -bl uf2-split-left

Press reset button on the keyboard when asked.  Currently this is done by double-tapping the physical reset 

Disconnect the first half, connect the second one and repeat the process.


Make example for this keyboard (after setting up your build environment):

    make sofle/rev1:default
    make sofle/keyhive:default

Flashing example for this keyboard:

    make sofle/rev1:default:flash
    make sofle/keyhive:default:flash

Press reset button on he keyboard when asked.

Disconnect the first half, connect the second one and repeat the process.

See the [build environment setup](https://docs.qmk.fm/#/getting_started_build_tools) and the [make instructions](https://docs.qmk.fm/#/getting_started_make_guide) for more information. Brand new to QMK? Start with our [Complete Newbs Guide](https://docs.qmk.fm/#/newbs).

## Bootloader

Enter the bootloader in 3 ways:

* **Bootmagic reset**: Hold down the key at (0,0) in the matrix
* **Physical reset button**: Briefly press the button near the TRRS connector. Quickly double-tap if you are using Pro Micro.
* **Keycode in layout**: Press the key mapped to `QK_BOOT` if it is available
