# Safety Rules

This project must preserve the Innioasis Y2 stock firmware until recovery and backup are proven.

## Forbidden Without Explicit Approval and Verified Recovery

- Do not flash the device.
- Do not erase partitions.
- Do not format partitions.
- Do not unlock the bootloader.
- Do not write to the Y2 eMMC.
- Do not run Y1 installers, Y1 updaters, or Y1 ROMs on the Y2.
- Do not write to `/proc/tpd_keys_enable` on the real device.
- Do not assume Y1 firmware packages are compatible with Y2.

## Allowed Safe Work

- Offline firmware file analysis.
- Decompiled APK analysis.
- Rockbox source comparison.
- Patch drafting.
- Harmless Android app builds.
- Read-only MTKClient exploration only after checking the command.
- Documentation updates.

## Current Safe Strategy

Use the official Y2 firmware package and stock launcher decompile as references. Build toward an Android-hosted Rockbox APK or launcher path. Do not modify the real device until backup/recovery and installation paths are understood.

## Device-Specific Warning

The official Innioasis Y2 updater should be treated as recovery-only because it formats/updates once started. Do not run it casually.
