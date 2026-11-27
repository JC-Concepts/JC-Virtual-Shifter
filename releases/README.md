# Release assets

Compiled firmware images and desktop installers are **not stored in this repository**. They are attached to GitHub Releases and are curated by a private release workflow.

Each release should contain only:

- `JC-Virtual-Shifter-<version>.zip` — the single download for users, with folders for `Desktop/Windows`, `Desktop/macOS`, `Firmware/<board>`, and `Compliance`,
- `SHA256SUMS.txt` plus a detached signature for that ZIP,
- `JC-Virtual-Shifter-release-public.asc` — the public key used to verify the signature.

The ZIP itself contains the release manifest, SBOM, notices, license texts, and LGPL relink packages. Never add `.bin`, `.elf`, `.map`, `.msi`, `.exe`, `.dmg`, signing keys, or build metadata to this repository. The root `.gitignore` blocks the common filename patterns as a safety net.
