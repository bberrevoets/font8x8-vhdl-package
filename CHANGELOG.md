# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## Attributors

- Bert Berrevoets (<bert@berrevoets.net>) — Berrevoets Systems — maintainer since 2026
- Claude Opus 5.5 — co-author of the 2026 changes
- Jonas Julian Jensen — the VHDL generator ([jonasjj/font8x8-vhdl-package](https://github.com/jonasjj/font8x8-vhdl-package))
- Daniel Hepper, with 0xDEAD and Will Green — the fonts and original renderer ([dhepper/font8x8](https://github.com/dhepper/font8x8))

## [Unreleased]

### Added

Author: *Bert Berrevoets*

- AI agent setup: [AGENTS.md](AGENTS.md) as the single instruction file, a [CLAUDE.md](CLAUDE.md) stub that imports it,
  markdownlint (180 characters), Git LFS rules and this changelog.
- `AGENTS.md`: Cross-Repository section for DotMatrixVHDLandFPGACourse, the course work that defines
  `dot_matrix.types` and uses the generated package; the overview now dates Bert's fork (2021-03) and his course work
  (2022-12) separately.

### Changed

Author: *Bert Berrevoets*

- Left the jonasjj / dhepper fork network; default branch renamed from `master` to `main` (GitHub Flow).
- Merged the upstream changes made after the fork: jonasjj's `ROW_COUNT` / `COL_COUNT` macros in `render.c` (2021-07)
  and dhepper's U+003B comment fix in `font8x8_basic.h` (2019-06). The generated VHDL is unchanged by both.
- `charmap_pck.vhd` regenerated: its header now names this repository, as `render.c` has since 2021-03.
- `README` renamed to `README.md`: course link updated, download link on `main`, authors and license.

## 2021-03

### Changed

Author: *Bert Berrevoets*

- Download link in the README and the repository URL printed by `render.c` point to this repository.

## 2019-01 – 2019-09

### Added

Author: *Jonas Julian Jensen*

- `render.c` outputs a VHDL package with the 8x8 bitmaps of the lower 128 ASCII characters; the generated
  `charmap_pck.vhd` is committed; common types moved to the course's `dot_matrix.types`; comments for printable
  characters; README for the VHDLwhiz Dot Matrix course.

## 2012-02 – 2018-10

### Added

Author: *Daniel Hepper, 0xDEAD*

- The 8x8 bitmap fonts as C headers and a simple renderer (dhepper/font8x8), README on the character encoding, a
  missing include in the renderer.
