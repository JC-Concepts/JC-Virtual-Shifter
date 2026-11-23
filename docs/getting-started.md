# Getting started

JC Virtual Shifter has four parts:

1. an ESP32 board with two buttons,
2. an official firmware image flashed to that board,
3. the desktop app for setup and diagnostics,
4. your existing smart trainer and riding app.

## Steps

1. Choose your board in the [supported boards table](../README.md#supported-boards).
2. Wire two momentary buttons using the [wiring guide](wiring.md).
3. Download the matching firmware image from the [latest release](../../releases/latest) and verify the checksum.
4. [Flash the firmware](flashing.md).
5. Install the [desktop app](desktop-app.md) for Windows or macOS from the same release.
6. Connect over USB, pair your trainer in the app, and configure your virtual drivetrain.
7. Pair the shifter in your riding app as power source and controllable trainer.

## First boot

On first boot the shifter has no saved trainer and no Wi-Fi credentials. The onboard LED slowly blinks (red on RGB boards) until the desktop app connects. Connect over USB to set it up.

The active button pins are printed on the serial monitor at 115200 baud at startup.

## Daily use

- Gear 1 is the easiest; Shift Up makes pedalling harder.
- Both buttons within 50 ms toggle the virtual front chainring when 2x front shifting is enabled.
- The current gear is not saved across power cycles; the configured start gear is loaded at boot.
- In SIM/route mode, gears change resistance. In ERG mode, your app controls target power.

See [troubleshooting](troubleshooting.md) if something does not behave as expected.
