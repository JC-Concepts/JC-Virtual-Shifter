# Release assets

Compiled firmware images and desktop installers are **not stored in this repository**. They are attached to GitHub Releases and are curated by the release workflow.

Each release should contain:

- firmware images for the board suffixes documented in the [supported boards table](../README.md#supported-boards),
- Windows and macOS desktop installers,
- `SHA256SUMS.txt` plus a detached signature,
- a release manifest with version, build identifier, board target, and toolchain versions.

Never add `.bin`, `.elf`, `.map`, `.msi`, `.exe`, `.dmg`, signing keys, or build metadata to this repository. The root `.gitignore` blocks the common filename patterns as a safety net.
