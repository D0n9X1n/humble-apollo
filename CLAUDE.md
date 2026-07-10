# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static Firefox **theme** WebExtension (Manifest V2) — no JavaScript, no background scripts. The
entire product is `manifest.json`'s `theme.colors` object. Firefox renders the browser chrome
directly from those color keys; there is nothing to compile or run.

The palette is [Gruvbox dark hard](https://github.com/morhetz/gruvbox). The theme name is
**Humble Apollo** (the repo/AMO identity — it is not related to the Apollo color palette). It is a
high-contrast dark theme built on the hard Gruvbox background (`#1d2021`), the warm cream foreground
(`#ebdbb2`), and the Gruvbox yellow accent (`#fabd2f`).

## Commands

No build step. Iterate by loading the manifest into Firefox:

- **Load / preview**: open `about:debugging#/runtime/this-firefox` → **Load Temporary Add-on…** →
  select `manifest.json`. Applies instantly; gone on restart.
- **Lint**: `web-ext lint` — validates `theme.colors` keys and manifest schema. Run this before
  committing color changes; unknown keys are silently ignored by Firefox but flagged here.
- **Package**: `web-ext build` → `web-ext-artifacts/humble_apollo-<version>.zip`. Rename to `.xpi`
  or submit to addons.mozilla.org for signing to install permanently.

## Working with colors

- Every value is a Gruvbox dark hard color — keep new values on-palette (see the swatch table in
  `README.md`, or the [Gruvbox reference](https://github.com/morhetz/gruvbox)) rather than
  introducing arbitrary hexes.
- Color keys map to specific chrome regions. Editing one key changes one region; there is no
  cascade. Key roles are grouped in `manifest.json` by region: frame/tabs, toolbar + URL field,
  icons, new-tab page (`ntp_*`), popups (`popup_*`), sidebar (`sidebar_*`).
- `toolbar_field*` = the address/search bar (darkest `bg0_h #1d2021`). `*_focus` variants apply when
  it's focused; the yellow `#fabd2f` accent marks focus/active borders, the tab line, and tab text.
- Contrast is intentionally maxed: brightest foreground `#fbf1c7`, lifted muted gray `#bdae93`, and
  `bg3 #665c54` borders against the `#1d2021` base. Preserve that separation when adjusting.
- `icons_attention`, `tab_loading`, `tab_text`, and focus borders all use Gruvbox yellow `#fabd2f`
  — the theme's single accent. Keep it consistent.
- Bump `version` in `manifest.json` for any released change; AMO rejects re-uploads of an existing
  version.
