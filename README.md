# JC Virtual Shifter

**Virtual shifting for your indoor trainer.** JC Virtual Shifter sits between a Bluetooth LE smart trainer and your indoor cycling app — such as TrainingPeaks Virtual, Zwift, MyWhoosh, or Rouvy — and adds handlebar shift buttons plus a configurable virtual drivetrain.

Shift up to make pedalling harder, shift down to make it easier, even on a trainer with no physical gears. A small desktop app handles setup, diagnostics, and an always-on-top HUD.

[Getting started](docs/getting-started.md) · [Wiring](docs/wiring.md) · [Flashing](docs/flashing.md) · [Desktop app](docs/desktop-app.md) · [Troubleshooting](docs/troubleshooting.md) · [Fair use](FAIR_USE.md)

---

## About this repository

This repository is the **public support and download home** for JC Virtual Shifter. It contains user documentation, release notes, and links to official download assets. It does **not** contain firmware or desktop application source code.

Official builds are published on the [Releases page](../../releases). Each release includes:

- firmware images for supported boards,
- Windows and macOS desktop installers,
- a `SHA256SUMS.txt` file and a detached signature,
- a release manifest with version and build identifier.

See [Verifying downloads](#verifying-downloads) below.

---

## What you need

| Item | Notes |
| :--- | :--- |
| ESP32 development board | ESP32-WROOM-32, ESP32-S3, or ESP32-C3. See [supported boards](#supported-boards). |
| 2 momentary push buttons | Tactile switches, bar-end clickers, or paddle shifters. |
| USB cable | Data-capable cable for flashing and first-time setup. |
| 5 V power | USB power is sufficient. |
| Bluetooth LE smart trainer | FTMS or FE-C control is required for virtual resistance. |
| Computer | Windows or macOS for the desktop app. |

A power-only trainer can still report power and cadence, but gears will not change resistance.

---

## Supported boards

Download the matching firmware image from the [latest release](../../releases/latest).

| Release asset suffix | Board | Shift Up | Shift Down |
| :--- | :--- | :--- | :--- |
| `esp32-wroom` | ESP32-WROOM-32 / classic DevKit | GPIO 18 | GPIO 5 |
| `esp32-s3-zero` | Waveshare ESP32-S3 Zero | GPIO 4 | GPIO 5 |
| `esp32-c3-mini` | LOLIN C3 Mini | GPIO 7 | GPIO 5 |

The pins above are built into the official images. No code edits are needed. See [wiring](docs/wiring.md) for LED pins, strapping-pin cautions, and assembly notes.

---

## Quick start

1. **Wire two buttons** to the pins for your board. See [wiring](docs/wiring.md).
2. **Download and verify** the firmware image and desktop installer from [Releases](../../releases/latest).
3. **Flash the firmware** with esptool. See [flashing](docs/flashing.md).
4. **Install the desktop app** on Windows or macOS. See [desktop app](docs/desktop-app.md).
5. **Connect over USB**, scan for your trainer, and pair it in the app.
6. **Pair the shifter in your riding app** as both power source and controllable trainer.
7. **Ride and shift.** Gear 1 is the easiest; Shift Up makes pedalling harder.

Pressing both buttons within 50 ms toggles the virtual front chainring when 2x front shifting is enabled.

---

## Verifying downloads

Every release publishes `SHA256SUMS.txt` and a detached signature.

**Windows (PowerShell):**

```powershell
Get-FileHash .\JC_Virtual_Shifter-<version>-esp32-wroom-merged.bin -Algorithm SHA256
Get-Content .\SHA256SUMS.txt
```

**macOS / Linux:**

```bash
shasum -a 256 -c SHA256SUMS.txt
gpg --verify SHA256SUMS.txt.sig SHA256SUMS.txt
```

The signing key fingerprint is published in the release notes. A matching hash confirms the file has not changed; the signature confirms it was produced by the release maintainer. Neither proves anything about firmware running on a board that someone else has flashed.

---

## Desktop app

The desktop app connects over USB serial, Wi-Fi, or Bluetooth LE setup and provides:

- trainer scanning and pairing,
- drivetrain and virtual cassette configuration,
- live diagnostics,
- an always-on-top HUD showing gear, ratio, and connection state.

Installers are currently **unsigned**. Windows SmartScreen and macOS Gatekeeper may warn on first launch; see [troubleshooting](docs/troubleshooting.md#installer-warnings).

---

## Riding with your training app

1. Wake the trainer and disconnect it from phones or other apps.
2. Confirm the desktop app shows the trainer as connected.
3. Pair the shifter in your riding app as power source and controllable trainer.
4. Start a ride.

In SIM/route mode, changing gear changes the resistance you feel. In ERG mode, your app keeps control of target power. Pair the trainer with the shifter only — if the riding app also connects directly to the trainer, the control link can be lost.

---

## Fair use

Official builds forward measured trainer power without multiplying it. Modified firmware is unsupported and may violate the rules of a riding platform or event. See [FAIR_USE.md](FAIR_USE.md).

---

## Like this Project?

You can buy me a gel, coffee, or inner tube. Your support helps me further develop on these types of projects.

[![](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RE2GQDK8CD2WW)

---

## Support and security

- Questions and bug reports: [Issues](../../issues)
- Security reports: [SECURITY.md](SECURITY.md) — please do not open a public issue.
- Privacy: [PRIVACY.md](PRIVACY.md)

---

## License

Documentation and distributed binaries are provided under the terms in [LICENSE.md](LICENSE.md). Third-party components are listed in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
