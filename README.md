# Humble Apollo — Firefox Theme

[![CI](https://github.com/D0n9X1n/humble-apollo/actions/workflows/ci.yml/badge.svg)](https://github.com/D0n9X1n/humble-apollo/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/D0n9X1n/humble-apollo?sort=semver)](https://github.com/D0n9X1n/humble-apollo/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/D0n9X1n/humble-apollo/total?logo=github&label=downloads)](https://github.com/D0n9X1n/humble-apollo/releases)
[![License: MIT](https://img.shields.io/github/license/D0n9X1n/humble-apollo)](LICENSE)
[![Firefox](https://img.shields.io/badge/Firefox-theme-FF7139?logo=firefoxbrowser&logoColor=white)](https://addons.mozilla.org/firefox/)
[![Manifest V2](https://img.shields.io/badge/manifest-v2-blue)](manifest.json)
[![Last commit](https://img.shields.io/github/last-commit/D0n9X1n/humble-apollo)](https://github.com/D0n9X1n/humble-apollo/commits/main)

A high-contrast dark Firefox theme based on the
[Gruvbox dark hard](https://github.com/morhetz/gruvbox) palette — the darkest Gruvbox background
(`#1d2021`) with the warm cream foreground and the signature yellow accent.

## Install / test locally

1. Open `about:debugging#/runtime/this-firefox` in Firefox.
2. Click **Load Temporary Add-on…**
3. Select `manifest.json` in this folder.

The theme applies immediately and is removed when Firefox restarts. Use this for iterating on colors.

## Package for distribution

Uses [`web-ext`](https://extensionworkshop.com/documentation/develop/getting-started-with-web-ext/)
via npm scripts (CI runs these on every push):

```sh
npm install
npm run lint      # validate manifest against the theme schema
npm run build     # produce web-ext-artifacts/humble_apollo-<version>.zip
```

## Releasing a new version

Releases are **automated by tag**. Pushing a `v*` tag triggers
[`.github/workflows/release.yml`](.github/workflows/release.yml), which lints, builds, and publishes
a GitHub Release with auto-generated notes (every commit since the previous tag) and the packaged
`.zip` attached.

```sh
# 1. Bump version in BOTH manifest.json and package.json (must match the tag), commit, push.
# 2. Tag and push it — the tag must equal the manifest version, prefixed with "v":
git tag v0.1.0
git push origin v0.1.0
```

The release job **fails if the tag doesn't match `manifest.json`'s `version`**, so the two can't
drift. Download the `.zip` from the published release, or grab it from the CI build artifacts.

### Publishing to Firefox (AMO)

Firefox only installs permanently-signed add-ons, and **[addons.mozilla.org](https://addons.mozilla.org)
(AMO) is the signer**.

1. Take the release `.zip` (or run `npm run build`).
2. Submit it:
   - **First release** — sign in at <https://addons.mozilla.org/developers/>, click *Submit a New
     Add-on*, upload the zip, choose **listed** (public on AMO) or **unlisted** (self-distributed
     `.xpi` you host), and fill in the listing (name, summary, screenshots, categories).
   - **Update** — open the add-on → *Manage* → *Upload New Version* → upload the new zip.
   - **CLI alternative** — generate API credentials at
     <https://addons.mozilla.org/developers/addon/api/key/> and run:
     ```sh
     npx web-ext sign --channel listed \
       --api-key "$AMO_JWT_ISSUER" --api-secret "$AMO_JWT_SECRET"
     ```
     `--channel listed` publishes on AMO; `--channel unlisted` returns a signed `.xpi` for
     self-hosting.
3. Listed submissions go through Mozilla review (themes are usually fast/automated). Once approved
   it's live at `addons.mozilla.org/firefox/addon/humble-apollo/`.

> The `browser_specific_settings.gecko.id` in `manifest.json` (`humble-apollo@d0n9x1n`) is the
> stable identity AMO ties every version to — don't change it between releases.

## Palette — Gruvbox dark hard

High-contrast dark theme built on the **hard** Gruvbox background (`#1d2021`), pushed for extra
contrast: the brightest cream foreground (`#fbf1c7`), a lifted muted gray (`#bdae93`), more-defined
borders (`#665c54`), and the signature Gruvbox yellow (`#fabd2f`) as the accent.

### Where each color goes

| Preview | Role | Hex |
| --- | --- | --- |
| ![](https://placehold.co/40x20/1d2021/1d2021.png) | Frame / URL bar / sidebar / new tab | `#1d2021` |
| ![](https://placehold.co/40x20/282828/282828.png) | Toolbar / selected tab | `#282828` |
| ![](https://placehold.co/40x20/3c3836/3c3836.png) | Popups / button hover | `#3c3836` |
| ![](https://placehold.co/40x20/665c54/665c54.png) | Borders / separators | `#665c54` |
| ![](https://placehold.co/40x20/fbf1c7/fbf1c7.png) | Foreground text | `#fbf1c7` |
| ![](https://placehold.co/40x20/bdae93/bdae93.png) | Muted text / icons | `#bdae93` |
| ![](https://placehold.co/40x20/fabd2f/fabd2f.png) | Accent (yellow) — tab text, focus, attention | `#fabd2f` |
| ![](https://placehold.co/40x20/7c6f64/7c6f64.png) | Highlight background | `#7c6f64` |

### Full Gruvbox dark hard reference

| | | | |
| --- | --- | --- | --- |
| ![](https://placehold.co/40x20/1d2021/1d2021.png) `bg0_h #1d2021` | ![](https://placehold.co/40x20/282828/282828.png) `bg0 #282828` | ![](https://placehold.co/40x20/3c3836/3c3836.png) `bg1 #3c3836` | ![](https://placehold.co/40x20/504945/504945.png) `bg2 #504945` |
| ![](https://placehold.co/40x20/665c54/665c54.png) `bg3 #665c54` | ![](https://placehold.co/40x20/7c6f64/7c6f64.png) `bg4 #7c6f64` | ![](https://placehold.co/40x20/a89984/a89984.png) `gray #a89984` | ![](https://placehold.co/40x20/ebdbb2/ebdbb2.png) `fg #ebdbb2` |
| ![](https://placehold.co/40x20/cc241d/cc241d.png) `red #cc241d` | ![](https://placehold.co/40x20/98971a/98971a.png) `green #98971a` | ![](https://placehold.co/40x20/d79921/d79921.png) `yellow #d79921` | ![](https://placehold.co/40x20/458588/458588.png) `blue #458588` |
| ![](https://placehold.co/40x20/b16286/b16286.png) `purple #b16286` | ![](https://placehold.co/40x20/689d6a/689d6a.png) `aqua #689d6a` | ![](https://placehold.co/40x20/fb4934/fb4934.png) `br-red #fb4934` | ![](https://placehold.co/40x20/fabd2f/fabd2f.png) `br-yellow #fabd2f` |
