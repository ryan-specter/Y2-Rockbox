# Beta V2 Updater Package Formats

Date: 2026-09-01

Status: **researched, built, reproducible, physically bound and approved for
publication**

## Decision

Beta V2 ships two Y2 firmware ZIPs:

1. `Y2-Rockbox-Beta-v0.2.0-InnioasisUpdater.zip`
   - Preserves the same top-level sparse-image package type as the previous
     Beta V1 release.
   - It is an outer rename of the exact physically accepted package; its bytes
     and SHA-256 are unchanged.
2. `rom_y2.zip`
   - Uses the canonical Y2 filename detected by Innioasis Updater CE and its
     GitHub release catalogue.
   - Contains the same accepted firmware payloads, with `system.img`,
     `cache.img` and `userdata.img` converted from Android sparse images to raw
     images for the cross-platform MTKClient path.
   - Adds the Y2 Download Agent and deterministic `history.ini` expected by the
     Updater CE packaging contract.

Both packages target only Innioasis Y2 hardware running the 3.1.7 lineage.
Neither is a Y1 package.

## Research basis

- Project issue #6 requests that the project retain the existing
  Innioasis-compatible release and additionally provide the canonical
  `rom_y2.zip` asset.
- Updater CE's developer documentation defines `rom_y2.zip` as the exact Y2
  full-install asset name and states that GitHub release assets, model and
  manifest entry together form its compatibility signal.
- Current Updater CE source identifies `rom_y2.zip` as Y2 before UI selection,
  applies the Y2 MT6582 scatter/preloader path, and lists the project through
  `slidia_manifest.xml`.
- The community mirror's build workflow converts sparse Android images to raw
  and packages the result as `rom_y2.zip`. The project-owned builder performs
  the same transformation directly from the exact accepted source package,
  avoiding mirror drift.

Primary references:

- <https://github.com/SPYCEMAGIC/Y2-Rockbox/issues/6>
- <https://github.com/y1-community/Innioasis-Updater/blob/main/developers.html>
- <https://github.com/y1-community/Innioasis-Updater/blob/main/slidia_manifest.xml>
- <https://github.com/y1-community/rockbox-y2-rom/blob/main/.github/workflows/mirror-release.yml>

## Immutable identities

### Previous-release/Innioasis format

- Size: 362,410,130 bytes
- SHA-256:
  `B9F0A4459B3C3DE0E9F5A6C99EC2F3246492EA065E43FF5996A5BEB0777D026E`

### Updater CE format

- Size: 370,911,657 bytes
- SHA-256:
  `22195AB5EF775585D73929C05B2FED28BB497C150705A91CC484A02308EB2A46`
- Member count: 57
- Repeat build: byte-identical

Raw-image identities:

| Image | Raw size | SHA-256 |
|---|---:|---|
| `system.img` | 859,832,320 | `805ED8A23E1DF13867C5EE789117CA90C6680779D20DD8884AD413DDD98FB00C` |
| `cache.img` | 132,120,576 | `E421AC0902F9C90DA56B0D078E8486F828AE4931358824E9F20839BBAFE9131B` |
| `userdata.img` | 837,812,224 | `B33B00B75643C5AD2FB0D62F493452CDAEF8C5A1AC16240CBFE9EE39AE4BCA7D` |

The raw `system.img` hash exactly matches P17's complete ANDROID physical
readback. Every non-transformed firmware member is byte-identical to the exact
physically accepted Innioasis-format package.

As of the final research check, Updater CE's catalogue still points the Y2
Rockbox entry at `y1-community/rockbox-y2-rom`. Upstream pull request #42
changes only that entry to `SPYCEMAGIC/Y2-Rockbox`; it should be marked ready
after the public release exposes the exact `rom_y2.zip` asset.

## Safety boundary

The public updater paths must be treated as full firmware installation paths
that can erase user data. Users must back up both storage volumes, the complete
`.rockbox` directory, themes, playlists, settings and databases before use.
They must verify checksums and retain the official Y2 3.1.7 recovery package.

The state-preserving five-target writer used during development remains a
controlled engineering tool. It is not represented as the behavior of every
public Updater CE or manufacturer-updater version.
