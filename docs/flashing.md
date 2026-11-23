# Flashing firmware

Always flash the image that matches your board. Flashing an S3 image to a WROOM board, or vice versa, will not work.

## 1. Get the image

Download the release asset whose suffix matches your board from the [latest release](../../releases/latest):

| Board | Asset suffix |
| :--- | :--- |
| ESP32-WROOM-32 / classic DevKit | `esp32-wroom` |
| Waveshare ESP32-S3 Zero | `esp32-s3-zero` |
| LOLIN S3 Mini and other S3 boards | `esp32-s3-generic` |
| LOLIN C3 Mini | `esp32-c3-mini` |
| ESP32-C3 Super Mini / generic C3 | `esp32-c3-supermini` |

Each release publishes either a `merged.bin` image or a set of split images (`bootloader.bin`, `partitions.bin`, `app.bin`). Verify the hash against `SHA256SUMS.txt` before flashing. See [verifying downloads](../README.md#verifying-downloads).

## 2. Install esptool

```bash
python -m pip install --upgrade esptool
```

## 3. Flash a merged image

A merged image contains the bootloader, partition table, and application in one file. Flash it at offset `0x0`.

**WROOM:**

```bash
esptool.py --chip esp32 --port COM3 --baud 921600 write_flash 0x0 JC_Virtual_Shifter-<version>-esp32-wroom-merged.bin
```

**Waveshare S3 Zero:**

```bash
esptool.py --chip esp32s3 --port COM3 --baud 921600 write_flash 0x0 JC_Virtual_Shifter-<version>-esp32-s3-zero-merged.bin
```

**LOLIN C3 Mini:**

```bash
esptool.py --chip esp32c3 --port COM3 --baud 921600 write_flash 0x0 JC_Virtual_Shifter-<version>-esp32-c3-mini-merged.bin
```

Replace `COM3` with your port (`/dev/cu.usbmodem...` on macOS). Release manifests list the exact chip and flash settings used for that build.

## 4. Flash split images

If a release provides split images, use the offsets for your chip:

| Chip | Bootloader | Partition table | Application |
| :--- | :--- | :--- | :--- |
| ESP32 (WROOM) | `0x1000` | `0x8000` | `0x10000` |
| ESP32-S3 | `0x0` | `0x8000` | `0x10000` |
| ESP32-C3 | `0x0` | `0x8000` | `0x10000` |

Example for WROOM:

```bash
esptool.py --chip esp32 --port COM3 --baud 921600 write_flash ^
  --flash_size 4MB --flash_mode qio ^
  0x1000 JC_Virtual_Shifter-<version>-esp32-wroom-bootloader.bin ^
  0x8000 JC_Virtual_Shifter-<version>-esp32-wroom-partitions.bin ^
  0x10000 JC_Virtual_Shifter-<version>-esp32-wroom-app.bin
```

On macOS/Linux use `\` line continuations instead of `^`. Match `--flash_mode` to the release manifest; WROOM builds use `qio`.

## 5. After flashing

- The board restarts and begins advertising over Bluetooth LE.
- Connect the desktop app over USB and pair your trainer. See [desktop app](desktop-app.md).
- Do not run `erase_flash` unless you are changing the partition layout or recovering from a failed flash. Erasing removes saved settings, including Wi-Fi credentials.
- A merged image is for a 4 MB flash board with the matching layout. Do not use it on an 8 MB board without checking the release manifest.

## Troubleshooting the flash

| Problem | What to try |
| :--- | :--- |
| No serial port appears | Use a data-capable cable, install the board's USB driver, try another port. |
| Upload fails | Hold BOOT while starting the flash, then release. Check the selected chip argument. |
| Board boots but buttons do nothing | Confirm you flashed the image for your chip family and check the [pin map](wiring.md#button-pins). |
| LED behaves unexpectedly | See the [LED table](wiring.md#onboard-status-led); C3 Mini and S3 variants differ. |
