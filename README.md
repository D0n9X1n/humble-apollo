# Humble Apollo — Firefox Theme

A dark Firefox theme based on the [Apollo color palette](https://lospec.com/palette-list/apollo)
(46 colors by AdamCYounis).

## Install / test locally

1. Open `about:debugging#/runtime/this-firefox` in Firefox.
2. Click **Load Temporary Add-on…**
3. Select `manifest.json` in this folder.

The theme applies immediately and is removed when Firefox restarts. Use this for iterating on colors.

## Package for distribution

With [`web-ext`](https://extensionworkshop.com/documentation/develop/getting-started-with-web-ext/):

```sh
web-ext lint      # validate manifest against the theme schema
web-ext build     # produce web-ext-artifacts/apollo-<version>.zip
```

Rename the resulting `.zip` to `.xpi` (or submit the `.zip` to
[addons.mozilla.org](https://addons.mozilla.org) for signing) to install permanently.

## Palette

A high-contrast dark theme, tuned like **Gruvbox dark hard** — backgrounds sink to the darkest
Apollo swatch and text/accents are lifted for sharper separation.

| Role              | Hex       |
| ----------------- | --------- |
| Frame / URL bar   | `#090a14` |
| Toolbar / tabs    | `#10141f` |
| Popups            | `#10141f` |
| Borders           | `#394a50` |
| Text              | `#ebede9` |
| Muted text/icons  | `#c7cfcc` |
| Accent (teal)     | `#a4dddb` |
| Attention (amber) | `#e8c170` |
