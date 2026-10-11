# font8x8-vhdl-package

This program generates a VHDL package containing a bitmap of the lower 128 ASCII characters.
It is intended for use with the [VHDLwhiz Dot Matrix](https://academy.vhdlwhiz.com/dotmatrix) VHDL course, whose
`dot_matrix.types` package defines the `charmap_type` used here.

## Usage

```sh
gcc -o render render.c && ./render > charmap_pck.vhd
```

Or just download the generated file:
<https://raw.githubusercontent.com/bberrevoets/font8x8-vhdl-package/main/charmap_pck.vhd>

See [dhepper/font8x8](https://github.com/dhepper/font8x8) for docs on the original program and fonts.

## Conventions

- **Branching:** GitHub Flow. `main` is protected and accepts changes only through pull requests.
- **Markdown:** linted with `markdownlint-cli2`, 180 character limit.

  ```sh
  npx markdownlint-cli2 "**/*.md"
  ```

- **Agent instructions:** in [AGENTS.md](AGENTS.md), read by Claude Code, Codex and any other coding agent.
  `CLAUDE.md` only imports it, so edit `AGENTS.md`.

## Authors

- Fonts and the original renderer: Daniel Hepper ([dhepper/font8x8](https://github.com/dhepper/font8x8)), based on
  IBM's public-domain VGA fonts; fixes by 0xDEAD and Will Green.
- VHDL generator: Jonas Julian Jensen ([jonasjj/font8x8-vhdl-package](https://github.com/jonasjj/font8x8-vhdl-package)).
- This repository (standalone since 2026-10-11): Bert Berrevoets — Berrevoets Systems — <bert@berrevoets.net>

License: Public Domain, as stated in the original README and the font headers.
