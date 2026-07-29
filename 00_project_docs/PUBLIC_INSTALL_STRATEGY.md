# Public Install Strategy

Date: 2026-07-14

## 2026-07-29 Beta v0.1.0 Addendum

The project is preparing an explicitly labelled Beta v0.1.0 from the
physically tested V88 full package. Since the original strategy was written,
V88 passed saved boot-route readback, playback, controls, sleep/wake, theme
persistence, internal and microSD playback, USB storage/return, power off and
official-stock rollback.

The apparent USB scaling report was resolved as SNAZZ3's intentional
30-pixel-margin layout. V89 remains physically untested and is not the beta
firmware.

The local beta asset folder contains:

- the byte-identical V88 firmware under a Beta v0.1.0 release filename;
- InnioasisUpdater 1.1.2, as directed by the project owner;
- an illustrated flashing, operation, USB and theme-install guide;
- a plain-text quick start;
- SHA-256 checksums;
- GPL/notice files; and
- a complete corresponding source archive containing the exact V88 Rockbox
  commit.

The beta prominently discloses destructive format-download flashing,
Bluetooth as untested, the unavailable both-volume fastboot chord, unresolved
date/time persistence and the unsigned updater executable. Generated vendor
and firmware assets remain out of Git history.

The public availability of the vendor updater and stock firmware is useful
provenance, but it does not by itself amend the third-party rights statement in
`NOTICE.md`. The project owner is responsible for confirming the terms of the
selected release host before uploading third-party binaries.

## Current Position

The current install path remains a firmware-package method for the Innioasis Y2. It
uses the official Y2 3.1.7 layout and flashes through the MediaTek restore lane.

V81 physically reached release behaviour except for its settings-save mailbox
boundary. V82's attempted `run-as` bridge failed physically and is rejected.
V83 replaces it with narrow caller-UID-gated Android IPC, has passed 18/18
dedicated offline checks plus generic validation, and now requires its physical
save/reboot and regression gate. Do not publish V83 as a general release until
that gate passes, the stock restore path is reconfirmed, and the
distribution/licensing questions below are resolved.

## Public Release Requirements

Already demonstrated on physical Y2 hardware:

- A readable and usable Rockbox UI on physical Y2 hardware.
- Basic input validation for wheel, previous/next, center, back, play/pause, and volume.
- Storage browsing for internal storage and microSD.
- At least one real audio playback pass.
- A tested restore path back to official stock firmware.
- A package validator that refuses Y1 payloads, critical-file changes, and unexpected firmware shapes.

Remaining public-release requirements:

- Pass the complete V83 route, settings-save, reboot, animation, power, theme, and USB
  regression gate.
- Reconfirm official-stock restore after the final candidate.
- Produce an end-user flow that does not redistribute vendor firmware without a clear
  legal basis.
- Publish the Rockbox fork from a reachable repository and update the parent
  submodule URL.
- Retain the documented GPL-2.0-or-later license for the parent repository's
  original scripts and documentation.
- Clear warnings that the current full-restore flow can erase user data.

## Flasher Direction

Do not start by building a custom flasher.

Near-term public use should prefer a patcher/packager that:

- asks the user to provide their own official Y2 firmware package,
- verifies hashes and expected Y2 markers,
- injects Rockbox into `system.img`,
- emits a validated modified package,
- instructs the user to use the existing vendor/MediaTek restore workflow.

A custom flasher only makes sense after the package format, restore path, and device detection are boring and repeatable. Until then, wrapping flash writes increases risk without solving the current Rockbox integration blockers.

## Legal And Identity Hygiene

Repository files and generated public docs should avoid personal names, local usernames, home directories, and machine-specific paths.

Public release artifacts should avoid redistributing Innioasis firmware unless there is a clear legal basis. A user-side patcher is safer because it can transform firmware the user already has instead of hosting vendor images.

Do not describe the method as an exploit in public-facing docs unless there is a concrete vulnerability being disclosed. The current method is better described as a firmware-package modification using the vendor restore path.

## Recommended GitHub Publication Sequence

1. Retain GPL-2.0-or-later for the parent repository's original code and
   documentation, and preserve every third-party notice.
2. Publish the modified Rockbox fork first, preserve its upstream history and license,
   and replace the parent repository's submodule URL with that reachable fork.
3. Create a clean public parent repository containing source, patches, build tools,
   validators, public documentation and small non-private validation summaries.
4. Exclude Innioasis firmware, generated firmware images/ZIPs, APKs, raw dumps,
   physical debug evidence, third-party tool binaries, local paths and personal data.
5. Run a full-history secret and large-file audit. If the current history contains
   vendor binaries or private captures, publish from a reviewed clean history rather
   than pushing the private development history.
6. Add a user-side patcher that verifies an official 3.1.7 package supplied by the
   user, applies the reviewed Rockbox changes and validates the emitted package.
7. Use GitHub Releases for the patcher, checksums, signed manifests and release notes;
   do not attach a vendor-derived full firmware ZIP unless redistribution permission
   has been established.
8. Add CI that builds or structurally validates the public artifacts, then tag the
   first release only after the complete physical V83 gate and official rollback pass.

This publishes the work as open source without treating vendor firmware or private
device evidence as project source. Publishing only a flashable binary would be less
auditable and would not solve the firmware-redistribution question.

## Open Questions

- Whether Innioasis firmware redistribution is permitted.
- Whether a minimal patch bundle can be generated against stock `system.img` instead of distributing a whole modified `system.img`.
- Whether the final install flow should preserve user data or continue using the full restore package shape.
- Whether future builds can use a stock launcher entry instead of delayed auto-launch.
