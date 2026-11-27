# Troubleshooting

## Connection and flashing

| Problem | What to check |
| :--- | :--- |
| No serial port appears | Use a data-capable cable, try another port, install the ESP32 USB driver. Click Refresh ports. |
| Flashing fails or board not detected | Hold BOOT while starting the flash, select the correct port, and confirm you are using the image for your chip. |
| Board resets or buttons do nothing | Check the [pin map](wiring.md#button-pins) and confirm you flashed the matching board image. |
| Gears feel backwards | Gear 1 is the easiest. Check which button is wired to Shift Up for your board. |
| 2x front shifting does not work | Enable 2x front shifting on the Drivetrain page, then press both buttons within 50 ms. |

## Trainer and riding app

| Problem | What to check |
| :--- | :--- |
| Trainer not found in the app | Wake the trainer, disconnect it from phones or other apps, and scan again. Use Show all BLE devices. |
| Trainer connects but resistance never changes | The trainer may be power-only. Virtual resistance needs FTMS or FE-C control. Also check that the riding app is in SIM/route mode, not ERG. |
| Riding app does not see the shifter | Pair the trainer in the desktop app first, confirm the shifter is powered, and close any other app holding the trainer's Bluetooth connection. |
| Settings cannot be applied | Reconnect over USB or Wi-Fi and read the current state first. Configuration needs an active connection. |

## Wi-Fi

| Problem | What to check |
| :--- | :--- |
| Shifter not found on Wi-Fi | Confirm both devices are on the same 2.4 GHz network, allow the app through the firewall, and enter `vshifter-xxxx.local` or the IP address with port 8266. |
| Wi-Fi setup fails | Use WPA2-PSK, disable client isolation, and keep the computer near the shifter during setup. |
| SoftAP fallback | Join `VC-Setup-XXXX` and connect to `192.168.4.1` on port 8266. |

## HUD

| Problem | What to check |
| :--- | :--- |
| HUD does not stay on top | Use Ctrl + Shift + H (Windows) or Cmd + Shift + H (macOS), or launch it from the sidebar. On macOS, check window permissions. |
| HUD shows stale values | Keep the desktop app connected over USB or Wi-Fi while riding. |

## Installer warnings

Official installers are currently unsigned.

- **Windows:** SmartScreen may show "Windows protected your PC". Choose **More info → Run anyway** only if the installer came from an official release ZIP you verified with `SHA256SUMS.txt` before extraction.
- **macOS:** Gatekeeper may say the app cannot be opened. If you downloaded the official release ZIP and verified it, right-click the app and choose **Open**, or remove the quarantine attribute:

  ```bash
  xattr -d com.apple.quarantine /path/to/JC\ Virtual\ Shifter.app
  ```

Unsigned builds are a distribution limitation, not a security feature. Never bypass these warnings for a file from an unknown source.

## Still stuck?

Open an [Issue](../../issues) with your board model, release version, operating system, and the steps to reproduce. For security concerns, use [SECURITY.md](../SECURITY.md) instead.
