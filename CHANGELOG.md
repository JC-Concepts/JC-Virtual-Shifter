# Changelog

All notable public releases of **JC Virtual Shifter** are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

First public release package is being prepared. Download assets will appear on the [Releases page](../../releases).

## [0.1.0] - 2026-11-20

### Added

- **Version reporting**: firmware reports a firmware version, protocol version, chip family, and build identifier; the desktop app displays them.
- **Wi-Fi control and setup**: Wi-Fi TCP control channel, local discovery, BLE and USB provisioning, and an open SoftAP fallback for first-time setup.
- **Desktop application**: configuration screens for the virtual drivetrain, cassette builder, diagnostics view, and an always-on-top HUD for Windows and macOS.
- **Firmware features**: Bluetooth LE bridge between FTMS/FE-C trainers and riding apps, discrete virtual gears, 2x virtual front shifting with a 50 ms button chord, and persistent settings.
- **Board support**: compile-time pin maps and official images for ESP32-WROOM, ESP32-S3, and ESP32-C3 families.

### Changed

- Documentation reorganized into a support-focused public repository with official binaries distributed through GitHub Releases.

### Fixed

- Button press edge cases and resistance scaling behavior in simulation mode.
- Bluetooth connection stability and macOS local-network permission handling.
