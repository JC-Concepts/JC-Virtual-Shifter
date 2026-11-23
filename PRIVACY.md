# Privacy

JC Virtual Shifter is a local device and desktop application.

- Telemetry flows between your trainer, the ESP32, the desktop app, and your riding app. The project does not operate a cloud service and no analytics or cloud telemetry were found in the distributed application.
- The desktop app requests Bluetooth and local network access on your computer so it can find the shifter and trainer.
- Wi-Fi network name and password, drivetrain settings, and paired trainer details are stored locally in the ESP32's non-volatile storage.
- The diagnostic console may display the configured network name. It does not display the stored Wi-Fi password.
- Flashing a used board without erasing it can leave previously stored settings in place.

If you sell or give away a board, erase its flash before handing it over.

Operating system installer warnings for unsigned builds are described in [troubleshooting](docs/troubleshooting.md#installer-warnings).
