#  PC Engine for Analogue Pocket with support for Analogizer-FPGA adapter

* Analogizer V1.1.0 [05/01/2024]: Added support for 2btn, 6btn PC Engine native game controllers and 5 Player Multi Tap
* Analogizer v1.1.1 [01/02/2025]: Added support for PSX SNAC game controllers. Added latest fixed by **agg23** to the Pocket core. Improved scandoubler SVGA video output.
Adapted to Analogizer by [@RndMnkIII](https://github.com/RndMnkIII) based on **agg23** PC Engine for Analogue Pocket Core.

The core can output RGBS, RGsB, YPbPr, Y/C and SVGA scandoubler (50% scanlines) video signals.

| Video output | Status | SOG Switch(Only R2,R3 Analogizer) |
| :----------- | :----: | :-------------------------------: |     
| RGBS         |  ✅    |     Off                           |
| RGsB         |  ✅    |     On                            |
| YPbPr        |  ✅🔹  |     On                            |
| Y/C NTSC     |  ✅    |     Off                           |
| Y/C PAL      |  ✅    |     Off                           |
| Scandoubler  |  ✅    |     Off                           |

🔹 Tested with Sony PVM-9044D

| :video_game:            | Analogizer A/B config Switch | Status |
| :---------------------- | :--------------------------- | :----: |
| DB15                    | A                            |  ✅    |
| NES                     | A                            |  ✅    |
| SNES                    | A                            |  ✅    |
| PCENGINE                | A                            |  ✅    |
| PCE MULTITAP            | A                            |  ✅    |
| PSX DS/DS2 Digital DPAD | B                            |  ✅    |
| PSX DS/DS2 Analog  DPAD | B                            |  ✅    |

The Analogizer interface allow to mix game inputs from compatible SNAC gamepads supported by Analogizer (DB15 Neogeo, NES, SNES, PCEngine, PSX) with Analogue Pocket built-in controls or from Dock USB or wireless supported controllers (Analogue support).

All Analogizer adapter versions (v1, v2 and v3) has a side slide switch labeled as 'A B' that must be configured based on the used SNAC game controller.
For example for use it with PSX Dual Shock or Dual Shock 2 native gamepad you must position the switch lever on the B side position. For the remaining
game controllers you must switch the lever on the A side position. 
Be careful when handling this switch. Use something with a thin, flat tip such as a precision screwdriver with a 2.0mm flat blade for example. Place the tip on the switch lever and press gently until it slides into the desired position:
```
     ---
   B|O  |A  A/B switch on position B
     ---   
     ---
   B|  O|A  A/B switch on position A
     ---
``` 
The following options exist in the core menu to configure Analogizer:
* **SNAC Adapter** List: None, DB15,NES,SNES,PCE,PCE Multitap, SNES swap A,B<->X,Y buttons, PSX (Digital DPAD), PSX (Analog DPAD).
* **SNAC Controller Assignment** List: several options about how to map SNAC controller to P1 Pocket controls. The controls not mapped to SNAC by default will map to Pocket connected controllers (Pocket built-in or Dock).
* **Analogizer Video Out** List: you can choose between RGBS (VGA to SCART), RGsB (works is a PVM as YPbPr but using RGB color space), YPbPr (for TV with component video input),
Y/C NTSC or PAL (for SVideo o compositive video using Y/C Active adapter by Mike S11), RGBHV for SVGA monitor Scandouble video output.

* **Analogizer** is responsible for generating the correct encoded Y/C signals from RGB and outputs to R,G pins of VGA port. Also redirects the CSync to VGA HSync pin.
The required external Y/C adapter that connects to VGA port is responsible for output Svideo o composite video signal using his internal electronics. Oficially
only the Mike Simone Y/C adapters (active) designs will be supported by Analogizer and will be the ones to use.

Support native PCEngine/TurboGrafx-16 2btn, 6 btn gamepads and 5 player multitap using SNAC adapter
and PC Engine cable harness (specific for Analogizer). Many thanks to [Mike Simone](https://github.com/MikeS11/MiSTerFPGA_YC_Encoder) for his great Y/C Encoder project.

For output Y/C and composite video you need to select in Pocket's Menu: `Analogizer Video Out > Y/C NTSC` or `Analogizer Video Out > Y/C NTSC,Pocket OFF`. You can tune the phase accumulator
with `Chroma Add` and `Chroma Multiply` sliders adjusting values between 0 and 31. Find the best match for your screen.

For output Scandoubler SVGA video you need to select in Pocket's Menu: `Analogizer Video Out > Scandoubler RGBHV`.

You will need to connect an active VGA to Y/C adapter to the VGA port (the 5V power is provided by VGA pin 9). I'll recomend one of these (active):
* [MiSTerAddons - Active Y/C Adapter](https://misteraddons.com/collections/parts/products/yc-active-encoder-board/)
* [MikeS11 Active VGA to Composite / S-Video](https://ultimatemister.com/product/mikes11-active-composite-svideo/)
* [Active VGA->Composite/S-Video adapter](https://antoniovillena.com/product/mikes1-vga-composite-adapter/)

Using another type of Y/C adapter not tested to be used with Analogizer will not receive official support.

I'll recomend also read this guide for MiSTer FPGA but can applied to Analogizer:
[MiSTer FPGA Documentation: Using Your CRT With MiSTer](https://mister-devel.github.io/MkDocs_MiSTer/advanced/crt/)

See Analogizer repository:
https://github.com/RndMnkIII/Analogizer

Because using the Analogizer adapter you are free to mix native gamepads+SNAC Adapter+Analogizer with Pocket inputs and/or DOCK gamepads, you need to enable 'Use Turbo Tap' or 'Use 6 Button Ctrl' options in the Pocket Core Menu.
Wether you are going to use native controls with SNAC or whether you are going to use the default controls of the Pocket or controls connected through the Dock. Later you have the "SNAC Controller Assignment" option that allows you to reassign the SNAC game controllers to the players you want, mixing them with non-SNAC controllers if you wish, or only use SNAC controllers. This depends on the type of controller and adapter you have, you will have the possibility of using 1,2 or up to 4 SNAC controllers. If your native PC Engine gamepads have Turbo buttons you don't need to enable the Core menu "Button I Turbo" or "Button II Turbo" options, directly turn on Turbo on the gamepad.

Ported from the core originally developed by [Gregory Estrade](https://github.com/Torlus/FPGAPCE) and heavily modified by [@srg320](https://github.com/srg320) and [@greyrogue](https://github.com/greyrogue). Core icon based on TG-16 icon by [spiritualized1997](https://github.com/spiritualized1997). Latest upstream available at https://github.com/MiSTer-devel/TurboGrafx16_MiSTer

Please report any issues encountered to this repo. Most likely any problems are a result of my port, not the original core. Issues will be upstreamed as necessary.


## Installation

### Easy mode

I highly recommend the updater tools by [@mattpannella](https://github.com/mattpannella) and [@RetroDriven](https://github.com/RetroDriven). If you're running Windows, use [the RetroDriven GUI](https://github.com/RetroDriven/Pocket_Updater), or if you prefer the CLI, use [the mattpannella tool](https://github.com/mattpannella/pocket_core_autoupdate_net). Either of these will allow you to automatically download and install openFPGA cores onto your Analogue Pocket. Go donate to them if you can

### Manual mode
Download the core by clicking Releases on the right side of this page, then download the `agg23.*.zip` file from the latest release.

To install the core, copy the `Assets`, `Cores`, and `Platform` folders over to the root of your SD card. Please note that Finder on macOS automatically _replaces_ folders, rather than merging them like Windows does, so you have to manually merge the folders.

## Usage

ROMs should be placed in `/Assets/pce/common`

SuperGrafix games **_MUST_** have the `.sgx` extension, as otherwise there's no way for the core to tell that it uses the SuperGrafx hardware.

Please note that CD games are not currently supported. Support will be added in a future update.

## Features

### Dock Support

Core supports four players/controllers via the Analogue Dock. To enable four player mode, turn on `Use Turbo Tap` setting.

### 6 button controller

Some games support a 6 button controller. For those games, enable the `Use 6 Button Ctrl` option in `Core Settings`. Please note that this option can break games that don't support the 6 button controller, so turn it off if you're not using it.

### Controller Turbo

Like the original PC Engine controllers, this core supports multiple turbo modes. Adjust the `I` and `II` button turbo modes, and use the `X` and `Y` buttons (by default) as your turbo buttons. Note that the original PCE controllers had the turbo on the `I` and `II` buttons directly, rather than having separate buttons, but since the Pocket has more than just two, we use them for the turbo.

### Video Modes

The PC Engine is unique in that it can arbitrarily decide what resolution to display at. The Pocket is more limited, requiring fixed resolutions at all times. I've tried to compromise and cover the most common resolutions output by the PCE, but some are better supported than others. You should see the video centered on the screen with surrounding black bars on some resolutions, but the aspect ratios should be correct.

### Video Options

* `Extra Sprites` - Allows extra sprites to be displayed on each line. Will decrease flickering in some games
* `Raw RGB Color` - Use the raw RGB color palette output by the HUC6260. If disabled, will use the composite color palette

### Audio Options

The core can be quiet in some games, so there are options to boost the master audio (`Master Audio Boost`) and ADPCM channels (`PCM Audio Boost`).

### Memory Cards

Instead of sharing a memory card (as you would in real life), each game gets its own save file and therefore memory card. Some games don't have the ability to initialize a memory card, so each newly created save file is pre-initialized for use.

## Licensing

All source included in this project from me or the [MiSTer project](https://github.com/MiSTer-devel/TurboGrafx16_MiSTer) is licensed as GPLv2, unless otherwise noted. The original source for [FPGAPCE](https://github.com/Torlus/FPGAPCE), the project this core is based off of, is [public domain](https://twitter.com/Torlus/status/1582663978068893696). The contents of the public domain tweet are reproduced here:

> Indeed. The main reason why I haven't provided a license is that I didn't know how to deal with the different licenses attached to parts of the cores.
Anyway, consider *my own* source code as public domain, i.e do what you want with it, for any use you want. (1/2)

[Additionally, he wrote](https://twitter.com/Torlus/status/1582664299973341184):

> If stated otherwise in the comments at the beginning of a given source file, the license attached prevails. That applies to my FPGAPCE project (https://github.com/Torlus/FPGAPCE).