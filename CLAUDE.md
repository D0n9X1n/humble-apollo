# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static Firefox **theme** WebExtension (Manifest V2) — no JavaScript, no background scripts. The
entire product is `manifest.json`'s `theme.colors` object. Firefox renders the browser chrome
directly from those color keys; there is nothing to compile or run.

The palette is [Apollo](https://lospec.com/palette-list/apollo) (46 colors). The theme name is
**Humble Apollo**. It is a high-contrast dark theme tuned like **Gruvbox dark hard**: backgrounds
sink to the darkest swatch (`#090a14`) and text/icons/accents are lifted for sharper separation.

## Commands

No build step. Iterate by loading the manifest into Firefox:

- **Load / preview**: open `about:debugging#/runtime/this-firefox` → **Load Temporary Add-on…** →
  select `manifest.json`. Applies instantly; gone on restart.
- **Lint**: `web-ext lint` — validates `theme.colors` keys and manifest schema. Run this before
  committing color changes; unknown keys are silently ignored by Firefox but flagged here.
- **Package**: `web-ext build` → `web-ext-artifacts/humble_apollo-<version>.zip`. Rename to `.xpi`
  or submit to addons.mozilla.org for signing to install permanently.

## Working with colors

- Every value must be a color the palette defines — keep new values on-palette (see the table in
  `README.md`) rather than introducing arbitrary hexes.
- Color keys map to specific chrome regions. Editing one key changes one region; there is no
  cascade. Key roles are grouped in `manifest.json` by region: frame/tabs, toolbar + URL field,
  icons, new-tab page (`ntp_*`), popups (`popup_*`), sidebar (`sidebar_*`).
- `toolbar_field*` = the address/search bar (darkest swatch `#090a14`). `*_focus` variants apply
  when it's focused; the teal `#73bed3` accent marks focus/active borders and the tab line.
- `icons_attention` and `tab_loading` use the amber `#e8c170` — that is the theme's one warm accent
  against the cool navy base. Preserve that contrast when adjusting.
- Bump `version` in `manifest.json` for any released change; AMO rejects re-uploads of an existing
  version.
