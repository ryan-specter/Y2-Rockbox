# Y2 Rockbox Beta V2 Release

Date: 2026-09-01

Tag: `v0.2.0-beta`

Status: **physically accepted and approved for publication**

## Release identity

Beta V2 is the corrected P17 Centre Context V1 runtime. It retains the complete
physically accepted P15/P16 baseline and changes only
`/system/app/Rockbox.apk`; the native core and full Rockbox resources remain
byte-identical. The APK and firmware package each reproduced twice, and the
exact candidate passed guarded installation, five complete readbacks and the
final focused physical regression.

Release ZIPs:

| Asset | Purpose | Size | SHA-256 |
|---|---|---:|---|
| `Y2-Rockbox-Beta-v0.2.0-InnioasisUpdater.zip` | Same sparse-image package type as Beta V1 | 362,410,130 | `B9F0A4459B3C3DE0E9F5A6C99EC2F3246492EA065E43FF5996A5BEB0777D026E` |
| `rom_y2.zip` | Canonical Updater CE Y2 package with raw Android images | 370,911,657 | `22195AB5EF775585D73929C05B2FED28BB497C150705A91CC484A02308EB2A46` |

The second ZIP is a deterministic packaging transform of the first. It does
not contain a different Rockbox build.

## Highlights since Beta V1

- Complete Bluetooth flow from Rockbox and Stock, including Settings access,
  discovery/pairing, A2DP playback, controls, disconnect and reconnect.
- Hold Previous/Next to seek within a track.
- Optional held-Volume track skipping with normal short-press volume behavior.
- Verified time/date and RTC persistence without UI freeze.
- Adjustable Rockbox wheel haptic intensity, including true-off, isolated from
  Stock's setting.
- Reliable first-connect and complete USB storage lifecycle on both routes.
- Stock overlay suppression during Rockbox USB and clean return/unplug/reconnect.
- Clean under-30-second SPYCE → Rockbox title → Rockbox root launch.
- Responsive Centre wake and improved Now Playing navigation/context controls.
- PictureFlow cache recovery and a functional album carousel.
- Reliable Boot Settings, saved Rockbox/Stock normal route and opposite-player
  Volume-Up route.
- State-preserving development updates plus physically proven Stock rollback,
  runtime recovery and protected-range integrity.

## Known limitations and Beta V3 direction

- The final power-down animation can render imperfectly. Shutdown itself is
  functional; presentation polish is a Beta V3 gate.
- FM is deferred until a Y2 vendor firmware baseline with demonstrably working
  radio is available.
- PictureFlow's branded missing-art slide and faster adjacent-cover loading are
  deferred polish.
- Beta V3 also targets lyrics/480x360 theme diagnostics, high-resolution FLAC
  stability, DAC and wired-audio qualification, Restart Rockbox/settings
  auditing, and database/playlist track-line presentation controls.
- Fastboot and a simultaneous-volume chord are not release features.

## Installation safety

Beta V2 is only for the Innioasis Y2 on the 3.1.7 firmware lineage. A Y1
package, another device's preloader, or another MediaTek scatter must never be
substituted.

Treat both public updater workflows as full firmware installs that can erase
the player:

1. Back up internal storage, microSD content, the complete `.rockbox` folder,
   settings, playlists, themes and database files.
2. Keep the official Y2 3.1.7 recovery package available.
3. Verify every release asset against `SHA256SUMS.txt`.
4. Charge the Y2, use a reliable data cable and avoid hubs.
5. Do not disconnect until the selected updater explicitly reports completion.

## Physical evidence

- P15 passed Rockbox boot, active/return USB, Stock isolation, three Boot
  Settings cold boots, saved-route dispatch and final sleep/wake.
- P16 passed official Stock rollback, protected-range comparisons, exact
  runtime reinstall with five complete readbacks, Stock regression and the
  complete final Rockbox/Stock/USB/route matrix.
- Final no-button boot reached a clean responsive Rockbox root in 28 seconds
  with no artifacts.
- Short Centre, the one-second long-Centre context menu with Bookmarks,
  no-release select-through, Centre sleep/wake, short Back to root and long
  Back to Database all passed on the exact corrected P17 runtime.
- Private device-unique protected hashes remain unpublished.

Device-unique readbacks and raw physical-test logs remain private. Their
release-facing results are summarized above without publishing identifiers or
protected partition hashes.
