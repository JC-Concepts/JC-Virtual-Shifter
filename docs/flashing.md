# Flashing firmware

Always flash the image that matches your board. The desktop app checks the connected chipset before writing, so a wrong image is rejected.

## 1. Get the image

Download the release asset whose suffix matches your board from the [latest release](../../releases/latest):

| Board | Asset suffix | Chip |
| :--- | :--- | :--- |
| ESP32-WROOM-32 / classic DevKit | `esp32-wroom` | ESP32 |
| Waveshare ESP32-S3 Zero | `esp32-s3-zero` | ESP32-S3 |
| LOLIN C3 Mini | `esp32-c3-mini` | ESP32-C3 |

Release assets are merged images (`*-merged.bin`): bootloader, partition table, and application in one file. Verify the hash against `SHA256SUMS.txt` before flashing. See [verifying downloads](../README.md#verifying-downloads).

## 2. Recommended: flash with the desktop app

You do not need Python or command-line tools.

1. Install the [desktop app](desktop-app.md) from the same release.
2. Connect the ESP32 to your computer with a **data-capable** USB cable.
3. Open **Diagnostics → ESP32 firmware flash**.
4. Select the serial port for your board. Click the refresh button if it is not listed.
5. Click **Select firmware (.bin)** and choose the downloaded `*-merged.bin` file.
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
