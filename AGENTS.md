# AGENTS.md

Instructions for AI coding agents (Claude Code, Codex and others) working in this repository. `CLAUDE.md` only imports
this file, so edit this one. [README.md](README.md) describes the project for people; this file lists what the code
alone does not tell you.

## Project Overview

A small C program, `render.c`, that turns the 8x8 bitmap font `font8x8_basic.h` into a VHDL package: `charmap_pck.vhd`
defines `package charmap` with the constant `charmap` (the lower 128 ASCII characters, 8 rows of 8 `std_logic` each).
The package uses `charmap_type` from `dot_matrix.types`, the library of the VHDLwhiz *Dot Matrix* VHDL/FPGA course
([academy.vhdlwhiz.com/dotmatrix](https://academy.vhdlwhiz.com/dotmatrix)). Bert forked it in March 2021; his work
from that course (December 2022) is in DotMatrixVHDLandFPGACourse (see Cross-Repository).

History: Daniel Hepper's [dhepper/font8x8](https://github.com/dhepper/font8x8) (C header fonts) → Jonas Julian
Jensen's [jonasjj/font8x8-vhdl-package](https://github.com/jonasjj/font8x8-vhdl-package) (the VHDL generator) →
this repository. It left the fork network on 2026-10-11 and is Bert's own since; both upstreams' later changes were
merged by hand that day (jonasjj's `ROW_COUNT`/`COL_COUNT` macros, dhepper's U+003B comment fix). Backup of the
pre-detach state: `E:\Backups\GitHub\font8x8-vhdl-package-2026-10-11`.

## Commands

```sh
gcc -o render render.c && ./render > charmap_pck.vhd      # Linux / Git Bash with gcc
```

On Bert's PC there is no gcc; use MSVC from a *Developer PowerShell / x64 Native Tools* prompt:
`cl /nologo render.c /Fe:render.exe` then `.\render.exe > charmap_pck.vhd`. The output is identical (checked on
2026-10-11). There are no tests: compare a regenerated `charmap_pck.vhd` with the committed one (`git diff`); the font
data must not change unless that is the point. Markdown lint: `npx markdownlint-cli2 "**/*.md"`.

## Repository Layout

```text
render.c            the generator: prints the VHDL package for font8x8_basic[0..127] to stdout
charmap_pck.vhd     the generated package, committed for people who don't want to compile (1,293 lines)
font8x8_basic.h     the font used (U+0000–U+007F)
font8x8_*.h         dhepper's other font tables (block, box, greek, hiragana, latin, ...) — not used by render.c
font8x8.h           includes all font tables
```

## Conventions

- `charmap_pck.vhd` is generated: change `render.c` and regenerate it, never edit the `.vhd` by hand. Commit both in
  the same commit.
- `charmap_type` is not defined here: it lives in the course's `dot_matrix.types` package (jonasjj moved the common
  types out of the generated file in 2019).
- Upstream changes: `jonasjj` and `dhepper` are configured as git remotes in Bert's clone with their **push URL set to
  `DISABLED`**. To take new upstream work: `git fetch jonasjj` / `git fetch dhepper`, then merge on a branch and open a
  PR. In a fresh clone, add them again with `git remote add` + `git remote set-url --push <name> DISABLED`.
- License: Public Domain — stated in dhepper's README and in the `font8x8_*.h` headers (the font data derives from
  IBM's public-domain VGA fonts); neither upstream has a `LICENSE` file.

## Cross-Repository

- [DotMatrixVHDLandFPGACourse](https://github.com/bberrevoets/DotMatrixVHDLandFPGACourse) (private;
  `D:\Repos\HardwareProjects\FPGA\DotMatrixVHDLandFPGACourse`): Bert's course work. It defines `dot_matrix.types`
  (`dot-matrix/src/packages/types_pck.vhd`, with `charmap_type`) and holds a copy of `charmap_pck.vhd` in the same
  folder, identical to this generator's 2021 output (the current file here differs only in the header URL). After
  regenerating here, copy the file there; when `charmap_type` changes there, check `render.c`.

<!-- repo-init:start -->
## Repository Info

- **Company:** Berrevoets Systems
- **Author:** Bert Berrevoets
- **Contact:** <bert@berrevoets.net>
- **Remote:** <https://github.com/bberrevoets/font8x8-vhdl-package> (public)

## Workflow Rules

- **GitHub Flow:** `main` is the default and only long-lived branch. It is protected by the ruleset "Protect main":
  no direct pushes, no deletion, changes only through a pull request, and all PR conversations must be resolved
  before merging. Merged head branches are deleted automatically.
- After cloning, run `git config pull.rebase true` once, so `git pull` rebases instead of creating merge commits.
- Work on a branch per topic, push it, and open a PR to `main` only when Bert asks for it, assigned to him
  (`gh pr create --assignee bberrevoets`). PRs are squash-merged. After a merge: switch to `main` and pull, then delete the
  local branch with `git branch -D <branch>` (`-d` refuses after a squash merge) once
  `gh pr view <branch> --json state,headRefOid` shows `MERGED` and the same commit as `git rev-parse <branch>`.
- **"Update the documentation"** means `AGENTS.md`, the project's own `README.md` files (not vendored third-party ones)
  and `CHANGELOG.md`; then commit and push.
- [CHANGELOG.md](CHANGELOG.md) follows Keep a Changelog: the Attributors list at the top, and one `Author: *Name*`
  line under each section heading (`### Added`, `### Changed`, ...).
- Markdown must pass `markdownlint-cli2 "**/*.md"` with [.markdownlint.json](.markdownlint.json) (180-character
  lines) before every commit.
- Binaries go through Git LFS: every `filter=lfs` pattern in `.gitattributes` — the standard set (PDF, ZIP, PNG,
  JPEG, STEP/STP, STL, 3MF, F3D/F3Z) plus any pattern this repository adds. Add a pattern there before committing
  another binary type (GIF, BMP, ...). The patterns are lowercase and match `X.PNG` only where `core.ignorecase` is
  true (Windows, macOS); on a case-sensitive system check a new binary with `git check-attr filter -- <file>` before
  committing it.
- Commit messages use the conventional style (`feat:`, `fix:`, `docs:`, `chore:`).
<!-- repo-init:end -->
