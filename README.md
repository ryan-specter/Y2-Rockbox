# Y2 RockBox

Rockbox for the Innioasis Y2, hosted inside its original Android 4.4.2
firmware. The project adds a full-screen Rockbox player, selectable cold-boot
routes, USB mass-storage return, and normal Rockbox theme support while
retaining the stock Y2 interface and its guarded updater/recovery path.

> [!WARNING]
> Firmware flashing can erase user data or make the player unbootable. This
> Beta V2 uses the exact physically accepted corrected P17 runtime. Verify the
> exact SHA-256 in the release notes before flashing.
> Innioasis Updater 1.1.2 has been proven to
> hardcode SP Flash Tool `format-download`; it is not a Download Only frontend.
> It erases the complete player. Do not use the rejected V84 three-partition
> ZIP with it.

## Supported hardware

The current build is only for:

```text
Device: Innioasis Y2
Official firmware: 3.1.7
Android: 4.4.2 / SDK 19
Platform: MediaTek MT6582
Board: eastaeon82_wet_kk
```

Do not use a Y1 package, a package for another Y2 firmware revision, or files
from a different MediaTek device.

## Current release status

Beta V2 is available as a GitHub prerelease:
<https://github.com/SPYCEMAGIC/Y2-Rockbox/releases/tag/v0.2.0-beta>.
Current compatibility reports are collected in
<https://github.com/SPYCEMAGIC/Y2-Rockbox/issues/9>.

Public beta releases use simple ordinal labels: **Beta V1** is the original V88
release, **Beta V2** is the current public release, and **Beta V3** is the next
planned beta. Existing branches and internal artifact names retain their
historical identifiers so recorded commands and hashes remain valid.

Beta V2's exact Innioasis-format package is 362,410,130 bytes at SHA-256
`B9F0A4459B3C3DE0E9F5A6C99EC2F3246492EA065E43FF5996A5BEB0777D026E`.
It was reconstructed byte-identically twice, installed through the guarded
P17 writer, and passed the complete cumulative Rockbox, Stock, Boot Settings,
USB, playback, sleep/wake and protected-state regression. The separate
Updater CE asset `rom_y2.zip` is deterministically derived from those same
payloads at SHA-256
`22195AB5EF775585D73929C05B2FED28BB497C150705A91CC484A02308EB2A46`.

## What is new in Beta V2

- Bluetooth Settings, pairing, A2DP playback, media controls, disconnect and
  reconnect work from both Rockbox and Stock.
- Holding Previous/Next seeks within a track. An optional setting lets held
  Volume buttons skip tracks while short presses continue to change volume.
- Time/date changes now write and read back the Y2 RTC without freezing the
  Rockbox UI.
- Rockbox wheel vibration is adjustable from true-off through multiple
  strengths while Stock keeps its independent haptic setting.
- First-connect USB Storage, active USB, safe eject, return, unplug and
  reconnect are stable on both routes without Stock overlays covering Rockbox.
- Clean SPYCE animation, a readable Rockbox title and responsive root complete
  in approximately 28 seconds on the accepted unit.
- Centre wake, improved Now Playing navigation, PictureFlow cache recovery,
  persistent Rockbox/Stock routing and Volume-Down Boot Settings are retained.
- Official Stock rollback, exact runtime recovery and protected-range
  preservation were physically proven before release.

Beta V3 is expected to concentrate on power-down presentation polish, lyrics
and broader 480x360 theme diagnostics, high-resolution FLAC stability, DAC and
wired-audio qualification, the Restart Rockbox/settings audit, database and
playlist line presentation, and the deferred PictureFlow loading polish. FM
work remains dependent on a demonstrably working Y2 vendor firmware baseline.

The complete Beta V2 release record and installer-format explanation are in
[Y2_ROCKBOX_BETA_V2_RELEASE.md](00_project_docs/Y2_ROCKBOX_BETA_V2_RELEASE.md)
and
[Y2_BETA_V2_UPDATER_FORMATS.md](00_project_docs/Y2_BETA_V2_UPDATER_FORMATS.md).

Beta V1 uses V88, the latest physically tested firmware. Saved-route
readback, playback, controls, sleep/wake, theme persistence, internal and
microSD playback, USB storage/return, the Stock route, power off and official
stock rollback passed physically.

The reported post-USB scaling concern was SNAZZ3's intentional layout. SNAZZ3
uses a 420-pixel menu viewport with 30-pixel side margins; MacClassic uses
almost the full 480x360 screen. V88's framebuffer remained full-size. V89 is
retained as an unflashed surface-lifecycle hardening experiment and is not the
beta release.

```text
Rejected: y2-v84-required-three-partition-update.zip
Reason: InnioasisUpdater formatted the full eMMC before the selective write
Physically rejected: y2-v85-simple-boot-choice-innioasis-full.zip
Reason: Boot Settings save requests timed out without a root acknowledgement
Physically rejected: y2-v86-boot-save-repair-innioasis-full.zip
Reason: Provider worked; route-map write used unavailable shell command printf
Physically rejected: y2-v87-vendor-shell-save-innioasis-full.zip
Reason: Save passed; early route-map reader still used unavailable printf
Beta V1 base: y2-v88-route-readback-repair-innioasis-full.zip
Release asset: Y2-Rockbox-Beta-v0.1.0-V88-InnioasisUpdater.zip
SHA-256: 40636D86943F6F0A1461B6D8C9285A1A50252253447B3DC7D11743533A88E4DE
Offline validation: 24/24 checks; byte-for-byte package reproduction passed
Physical saved-route readback: PASSED
Physical playback/controls/sleep/theme/storage/power: PASSED
Physical USB storage and Rockbox return: PASSED
Official-stock rollback: PASSED
Not in release: y2-v89-usb-display-restore-innioasis-full.zip
SHA-256: 58C7D205DFFD211F265515B840EC71A4283D126960D7E86D2632AA0A5361075B
Offline validation: 21/21 checks; generic package shape valid
Reproducibility: APK, system image, and full ZIP passed
Physical status: UNTESTED
```

V82, V83, V84's compatibility-gated UI, and the selective V84 ZIP are
rejected. V85 and V86 flashed successfully but failed their physical save
gates. The release decision and complete beta limitations are in
[Y2_ROCKBOX_BETA_V0.1.0_RELEASE.md](00_project_docs/Y2_ROCKBOX_BETA_V0.1.0_RELEASE.md).

## Back up before flashing

1. Copy all music and the complete `.rockbox` directory from both Y2 storage
   volumes to the computer.
2. Preserve any Boot Settings choices, playlists, database files, themes, and
   `config.cfg`.
3. Keep an extracted, hash-verified copy of the official Y2 3.1.7 restore
   package available.
4. Charge the Y2, use a reliable data cable, and avoid USB hubs.
5. Close programs that may claim MediaTek USB devices.

InnioasisUpdater uses SP Flash Tool `format-download`, so every candidate flash
must be treated as a full-device erase. Never rely on internal eMMC as the only
copy of music or settings.

## Flashing

Beta V2 provides two installable ZIPs containing the same accepted runtime:

- `Y2-Rockbox-Beta-v0.2.0-InnioasisUpdater.zip` retains the same sparse-image
  package type as Beta V1.
- `rom_y2.zip` is the canonical Updater CE package, with the Android images
  converted to raw form for the cross-platform path.

Use only one route and verify its published SHA-256. Full instructions are in
[Y2_ROCKBOX_BETA_V2_INSTALL_GUIDE.md](00_project_docs/Y2_ROCKBOX_BETA_V2_INSTALL_GUIDE.md).

Flashing is a real device write. Back up first, verify the exact SHA-256 above,
and follow the release guide without improvising retries.

## Beta V2 release assets

The release folder contains both firmware formats, `README-FIRST.txt`, the
Markdown install guide, the complete corresponding source archive, a sanitized
Updater CE packaging manifest, SHA-256 checksums, the legacy Windows updater,
and license/notice files. Updater CE itself remains available from its upstream
project and is not copied into this repository's source history.

## Historical Beta V1 release assets

The assembled beta folder is self-contained for installation. Users do not
need a separate scatter file, Download Agent, partition image or USB driver
bundle. It contains:

- `README-FIRST.txt`;
- the complete Y2 Rockbox Beta V1 firmware ZIP;
- `InnioasisUpdater_Setup_1.1.2.exe`, including its driver-install stage;
- an illustrated flashing, operation, USB and theme-install PDF;
- `SHA256SUMS.txt`;
- the complete corresponding source archive; and
- the project license and notice.

The firmware ZIP, flasher and other generated assets remain release attachments
rather than Git-tracked source files. The Windows updater is unsigned; users
must verify its published SHA-256 before running it.

## Cold-boot routes

Start from a fully powered-off Y2. For a button route, hold the button before
pressing Power and keep it held until the normal haptic release cue.

The default map after flashing is:

| Input | Default destination |
|---|---|
| No volume button | Rockbox |
| Volume Up | Y2 stock interface |
| Volume Down | Boot Settings |

Boot Settings changes only the normal-boot player. Volume Up automatically
becomes the other player. Volume Down is fixed and is not shown as a choice.
Simultaneously holding both volume buttons is unsupported and unassigned for
the beta; it is not a feature or an acceptance test.

## Boot Settings

Boot Settings contains one choice: what starts when no volume button is held.
The screen deliberately stays minimal; the complete button map is documented
here.

1. Cold boot with Volume Down using the default map.
2. Select **Rockbox** or **Y2 Stock** under **Normal boot**.
3. Select **Save & Restart**.
4. Require `Saving...`, followed by `Saved - restarting...`.
5. The Y2 should restart automatically into the selected normal-boot player.
6. Cold boot with Volume Up and require the other player.
7. Cold boot with Volume Down and require Boot Settings.

Saving the already-selected choice is valid and must still be written,
verified, acknowledged, and followed by an automatic restart. If Save times
out, does not restart, or boots with the old choice, stop testing and preserve
the complete SD debug folder.

Fastboot is not included or advertised as a beta feature. Do not depend on a
both-volume chord. Retain the proven powered-off guarded updater/pinhole restore
procedure for installation and recovery.

## Using Rockbox

- The centre button confirms selections and wakes the display.
- Previous/Next move left and right; the wheel moves through lists.
- Play/Pause controls playback; Back returns to the previous screen.
- Hold Power for roughly three seconds for the normal power action.
- Music is read from the Y2's internal storage and microSD.

After a first flash, allow Rockbox to finish its initial resource and storage
setup before forcing a restart or connecting USB.

## Installing themes

Use themes designed for a 480x360 Rockbox screen or known-compatible Y1
360p themes. A complete theme commonly includes files in several directories;
copying only its `.cfg` file is not enough.

1. Boot Rockbox and connect the Y2 to the computer.
2. On the Y2 USB-storage screen, enable USB storage. Rockbox may close while
   its storage is exported; that is expected.
3. Open the exposed internal-storage volume and enable hidden-file display.
4. Back up its existing `.rockbox` directory.
5. Extract the downloaded theme and merge its complete `.rockbox` directory
   into the existing directory at the root of internal storage. Typical paths
   include:

   ```text
   .rockbox/themes/
   .rockbox/wps/
   .rockbox/fonts/
   .rockbox/icons/
   .rockbox/backdrops/
   ```

6. Never replace or delete the whole existing `.rockbox` tree. Merge only the
   new theme's files.
7. Eject every Y2 volume safely on the computer, turn USB storage off if the
   Y2 screen requests it, and disconnect the cable.
8. Wait for storage to remount and Rockbox to return.
9. Open **Settings > Theme Settings > Browse Themes** (called
   **Browse Theme Files** in some builds), select the theme, then cold boot
   once to confirm it persists.

If Rockbox cannot find music or a theme after USB use, disconnect safely and
wait for storage to remount before restarting. Do not edit `.rockbox` while
Rockbox is actively using the volume.

## Recovery and troubleshooting

- Keep the official Y2 3.1.7 package and its original flashing instructions.
- Restore with the official complete Y2 package and its InnioasisUpdater
  instructions. The bottom reset/pinhole is the proven powered-off detection
  aid.
- Never substitute a preloader from another device.
- A black screen, repeated boot logo, wrong route, missing storage, save
  timeout, crash dialog, or failed power/USB behaviour is a stop condition.
- Power off before removing the diagnostic microSD.
- Copy the complete `Y2_V*_DEBUG` folder and the root marker/snapshot files
  without modifying them. Hash the copy before analysis.

Development evidence and large generated artifacts are deliberately ignored by
Git. See [SAFETY.md](00_project_docs/SAFETY.md) and
[PUBLIC_INSTALL_STRATEGY.md](00_project_docs/PUBLIC_INSTALL_STRATEGY.md) for
the engineering and distribution rules. The concrete pre-publication findings
are in
[PUBLIC_REPOSITORY_CLEANUP_20260726.md](00_project_docs/PUBLIC_REPOSITORY_CLEANUP_20260726.md).
The current release record is
[Y2_ROCKBOX_BETA_V2_RELEASE.md](00_project_docs/Y2_ROCKBOX_BETA_V2_RELEASE.md).

## Repository and licensing status

The public model is open source: publish the original source, patch/build
tools, validators and documentation, and attach the complete corresponding
source archive to the binary release. Do not commit vendor firmware, generated
firmware ZIPs, APKs, raw device dumps, private debug evidence or third-party
tools to the source repository.

Original parent-project code and documentation are licensed under
GPL-2.0-or-later; see [LICENSE](LICENSE) and [NOTICE.md](NOTICE.md). The
modified Rockbox submodule retains its upstream licenses. The Beta V1
asset set therefore includes the exact V88 Rockbox source commit as well as the
parent build and validation source. A reachable public repository remains the
preferred long-term source location.
