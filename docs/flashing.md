# Flashing firmware

Always flash the image that matches your board. The desktop app checks the connected chipset before writing, so a wrong image is rejected.

## 1. Get the image

Download and verify the release ZIP from the [latest release](../../releases/latest), then extract it. See [verifying downloads](../README.md#verifying-downloads).

Open the `Firmware/` folder and choose the folder that matches your board:

| Board | Firmware folder | Chip |
| :--- | :--- | :--- |
| ESP32-WROOM-32 / classic DevKit | `ESP32-WROOM-32` | ESP32 |
| Waveshare ESP32-S3 Zero | `ESP32-S3-Zero` | ESP32-S3 |
| LOLIN C3 Mini | `LOLIN-C3-Mini` | ESP32-C3 |

Each folder contains a merged image (`*-merged.bin`): bootloader, partition table, and application in one file, plus a `.sha256` sidecar. The signed `SHA256SUMS.txt` on the release page verifies the ZIP before extraction. See [verifying downloads](../README.md#verifying-downloads).

## 2. Recommended: flash with the desktop app

You do not need Python or command-line tools.

1. Install the [desktop app](desktop-app.md) from `Desktop/Windows` or `Desktop/macOS` in the extracted ZIP.
2. Connect the ESP32 to your computer with a **data-capable** USB cable.
3. Open **Diagnostics → ESP32 firmware flash**.
4. Select the serial port for your board. Click the refresh button if it is not listed.
5. Click **Select firmware (.bin)** and choose the `*-merged.bin` file from the matching `Firmware/` folder.
6. Optional: click **Detect device chip** to confirm the board chipset before flashing.
7. Click **Flash selected firmware** and confirm the prompt.

The app disconnects any active session, detects the connected chipset, checks that it matches the image, writes the image at offset `0x0`, and resets the board. Do not unplug the board while the progress bar is active. If the board does not reset automatically, press its RESET button, or hold BOOT when starting the flash.

## 3. After flashing

- The board restarts and begins advertising over Bluetooth LE.
- Connect the desktop app over USB and pair your trainer. See [desktop app](desktop-app.md).
- Do not run `erase_flash` unless you are recovering from a failed flash. Erasing removes saved settings, including Wi-Fi credentials.
- Merged images are built for 4 MB flash boards with the layout listed in the release manifest.

## Troubleshooting the flash

| Problem | What to try |
| :--- | :--- |
| No serial port appears | Use a data-capable cable, install the board's USB driver, try another port. |
| App reports a chipset mismatch | You selected the image for a different board. Download the matching asset. |
| Flash fails or board is not detected | Hold BOOT while starting the flash, then release. Check the USB cable and port. |
| Board boots but buttons do nothing | Confirm you flashed the image for your board and check the [pin map](wiring.md#button-pins). |
| LED behaves unexpectedly | See the [LED table](wiring.md#onboard-status-led). |
