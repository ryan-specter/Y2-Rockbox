# Y2 Rockbox Safety Rules

Updated: 2026-09-01

Firmware installation can erase user data or make the player unbootable.
Rockbox Y2 packages are device-specific.

## Never do this

- Do not flash a Y1 package, Y1 updater image or another device's preloader.
- Do not use a package for an unknown Y2 hardware or firmware revision.
- Do not write generated firmware until its input identity, partition layout,
  checksums and recovery path have been verified.
- Do not disconnect or reset the device while an updater is actively writing.
- Do not let an upstream-version check silently download, build, package or
  flash a different firmware.
- Do not publish device-unique protected data or raw private test evidence.

## Before installation

- Back up internal storage and microSD content.
- Back up the complete hidden `.rockbox` directory, including themes,
  playlists, settings and databases.
- Keep the official Innioasis Y2 3.1.7 recovery package available.
- Verify every release asset against `SHA256SUMS.txt`.
- Charge the player, use a reliable data cable and avoid USB hubs.
- Close software that may claim MediaTek USB devices.

## Supported public recovery boundary

Beta V2 targets only the Innioasis Y2 on the official 3.1.7 lineage. Both
published updater formats must be treated as full firmware installations.
The bottom reset/pinhole is a powered-off device-detection aid; it is not a
general retry button during a write.

Stop and use the documented official recovery path after a failed install,
persistent boot loop, wrong repeated route, missing storage or persistent
crash dialog. Never substitute recovery files from another device.

## Release evidence

A build is release-ready only after deterministic packaging, offline
validation, a guarded physical installation, complete readback, route and
playback regression, USB lifecycle tests, power/sleep tests and official Stock
rollback. Public summaries omit device identifiers and protected partition
hashes.
