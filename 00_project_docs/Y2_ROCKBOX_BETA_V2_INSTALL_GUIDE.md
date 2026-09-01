# Y2 Rockbox Beta V2 Installation and Use Guide

## Read before installing

Beta V2 supports only the Innioasis Y2 on the official 3.1.7 firmware lineage.
Do not use a Y1 package, another device's scatter/preloader, or a package for an
unknown Y2 hardware revision.

Firmware installation can erase the complete player. Before starting:

1. Back up both visible storage volumes.
2. Back up the complete hidden `.rockbox` directory, including themes,
   playlists, settings and databases.
3. Keep the official Y2 3.1.7 recovery package available.
4. Charge the player and use a reliable data cable without a USB hub.
5. Verify every downloaded file against `SHA256SUMS.txt`.

## Choose one installation route

### Innioasis Updater CE

Use the current Updater CE release from:

<https://github.com/y1-community/Innioasis-Updater/releases/latest>

Select **Y2** as the model, select **Rockbox**, select the Beta V2 release, and
follow the prompts. For a manually downloaded file, choose the release asset
named exactly `rom_y2.zip`. Do not rename a Y1 package to that filename.

### Previous-release/manufacturer-updater format

Use `Y2-Rockbox-Beta-v0.2.0-InnioasisUpdater.zip` with the same package-selection
flow used for Beta V1. The release also retains the previously supplied
`InnioasisUpdater_Setup_1.1.2.exe`; it is unsigned, so verify its exact SHA-256
before running it.

Treat both routes as full firmware installations. Do not disconnect until the
updater reports completion. If powered-off device detection does not begin when
prompted, leave the cable connected and gently press the bottom reset/pinhole
once. Do not improvise repeated resets while a write is active.

## First boot and route controls

Start with the Y2 fully powered off:

| Input while powering on | Destination |
|---|---|
| No Volume button | Saved normal route; Rockbox by default |
| Volume Up | The opposite player, Stock by default |
| Volume Down | Boot Settings |

In Boot Settings, choose the normal player and select **Save & Restart**. The
Volume-Up route automatically remains the opposite player. A simultaneous
Volume-button fastboot chord is not a Beta V2 feature.

The accepted no-button Rockbox boot shows SPYCE animation, a readable Rockbox
title, then the Rockbox root in approximately 28 seconds. The first boot after
a full installation may take longer while Android prepares application state.

## Rockbox controls added or refined in Beta V2

- Centre confirms selections, toggles play/pause on Now Playing, and wakes the
  sleeping display without selecting through.
- Hold Centre for about one second on Now Playing to open the standard context
  menu, including Bookmarks.
- Short Back/Menu from Now Playing returns to the Rockbox root. Hold Back/Menu
  to return to the previous browsing context.
- Hold Previous/Next to seek within the current track.
- Under Playback Settings, the Volume long-press option can make held Volume
  buttons skip tracks while short presses still change volume.
- Rockbox wheel-vibration strength includes a true-off setting and remains
  independent from Stock's key-vibration setting.

## Bluetooth

Open **Settings → Bluetooth** from Rockbox to enter Android Bluetooth Settings.
Pair the device normally, then return to Rockbox. Beta V2 passed A2DP playback,
Y2 controls, supported remote controls, disconnect pause and reconnect on the
accepted hardware. Stock uses the same retained Android bond.

## USB storage

Connect the cable and wait for the USB Storage screen. Enable storage only when
you need file access. Safely eject every mounted Y2 volume on the computer,
then turn storage off on the player before unplugging when that control is
shown. Rockbox does not automatically resume a paused track after USB; this is
normal.

## Themes and PictureFlow

Use complete 480x360 Rockbox themes. Merge a theme's complete `.rockbox`
subtree into the existing directory; do not replace or delete the whole tree.
PictureFlow's carousel is functional. Faster adjacent-cover loading and the
custom missing-art image are deferred polish.

## Recovery and stop conditions

Stop and use the documented official recovery path if installation fails, the
wrong route repeatedly opens, the device loops, storage disappears, or a crash
dialog persists. Keep the official 3.1.7 package and never substitute a
preloader from another device.

The known imperfect final power-down animation is visual: shutdown completed
throughout acceptance testing. Its presentation polish is scheduled for Beta
V3.
