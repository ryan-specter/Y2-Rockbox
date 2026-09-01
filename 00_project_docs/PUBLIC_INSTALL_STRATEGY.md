# Public Install Strategy

Updated: 2026-09-01

## Current Beta V2 distribution

Beta V2 publishes two full-install ZIPs containing the same physically accepted
runtime:

- `Y2-Rockbox-Beta-v0.2.0-InnioasisUpdater.zip` preserves the sparse-image
  package type used by Beta V1.
- `rom_y2.zip` is the canonical Y2 asset name for Innioasis Updater CE and
  contains raw Android system/cache/userdata images.

Both target only the Innioasis Y2 on the official 3.1.7 firmware lineage. They
must be treated as full firmware installations that can erase user data. The
release includes SHA-256 checksums, an installation guide, a sanitized package
manifest and complete corresponding source.

Updater CE details and immutable hashes are recorded in
[Y2_BETA_V2_UPDATER_FORMATS.md](Y2_BETA_V2_UPDATER_FORMATS.md).

## Required user safeguards

Before installation, users must:

1. back up internal storage, microSD content and the complete hidden
   `.rockbox` directory;
2. preserve settings, themes, playlists and databases;
3. retain the official Y2 3.1.7 recovery package;
4. verify the selected release asset against `SHA256SUMS.txt`; and
5. use a charged player, reliable data cable and no USB hub.

A Y1 package, a package for another Y2 firmware lineage, or another MediaTek
preloader/scatter must never be substituted.

## Public source and history model

The public repository is a reviewed source snapshot. It contains public
documentation, relevant builders and validators, and a submodule pointing to
the exact accepted modified Rockbox source. Binary release assets remain in
GitHub Releases rather than Git history.

The private development history, raw device evidence, vendor images, generated
firmware, APKs and device-unique protected data are not published as Git source.
Each binary release instead carries a complete corresponding-source archive
with the exact parent and Rockbox commit identities used to assemble it.

## Next installer direction

The preferred long-term path is a user-side patcher/packager that:

- asks the user to provide their own official Y2 3.1.7 firmware;
- verifies its hashes, partition layout and Y2 identity;
- applies the reviewed Rockbox changes;
- produces and validates an installable package; and
- preserves user data where the platform permits it.

That work must not weaken the current recovery gate or silently download,
build, package or flash a different firmware. A custom flasher is not a
priority until device detection, package conversion, backup and restore are
boring and repeatable.

## Publication requirements

Every public binary release must include:

- a device/firmware compatibility warning;
- complete backup, install and recovery instructions;
- immutable checksums and a machine-readable manifest;
- the complete corresponding source and license notices;
- a clear list of physically accepted behavior and known limitations; and
- an explicit statement when an updater or installation route can erase data.

The project must not describe an experimental or merely offline-validated build
as physically accepted.
