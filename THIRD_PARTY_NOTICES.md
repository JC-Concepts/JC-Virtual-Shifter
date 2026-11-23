> **DRAFT — complete this from the release SBOM before the first binary release.**

# Third-party notices

Official JC Virtual Shifter binaries include third-party components. Their licenses and notices apply to those components and are not replaced by the project license.

| Component | Used in | License | Upstream |
| :--- | :--- | :--- | :--- |
| NimBLE-Arduino | Firmware BLE stack | Apache License 2.0 | https://github.com/h2zero/NimBLE-Arduino |
| Bounce2 | Firmware button debouncing | MIT | https://github.com/thomasfredericks/Bounce2 |
| Arduino-ESP32 core | Firmware build platform | LGPL-2.1-or-later | https://github.com/espressif/arduino-esp32 |
| ESP-IDF components | Firmware | Apache-2.0 and component-specific licenses | https://github.com/espressif/esp-idf |
| Tauri | Desktop application shell | MIT / Apache-2.0 | https://github.com/tauri-apps/tauri |
| React, Vite, TypeScript, Tailwind CSS | Desktop application UI | MIT | See each upstream project |
| Rust crates in the desktop build | Desktop application | See `Cargo.lock` | https://crates.io |
| npm packages in the desktop build | Desktop application UI | See `package-lock.json` | https://www.npmjs.com |

The Arduino-ESP32 core is LGPL-2.1-or-later. Static linking into a distributed firmware image carries notice and source/relink obligations for that component; confirm the exact compliance path before the first binary release.

Before a release is published, generate a complete SBOM from the private build and place the resolved notices here. Include full license texts where the licenses require it.
