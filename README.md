# Humble Apollo — Firefox Theme

[![CI](https://github.com/D0n9X1n/humble-apollo/actions/workflows/ci.yml/badge.svg)](https://github.com/D0n9X1n/humble-apollo/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/D0n9X1n/humble-apollo?sort=semver)](https://github.com/D0n9X1n/humble-apollo/releases/latest)
[![License: MIT](https://img.shields.io/github/license/D0n9X1n/humble-apollo)](LICENSE)
[![Firefox](https://img.shields.io/badge/Firefox-theme-FF7139?logo=firefoxbrowser&logoColor=white)](https://addons.mozilla.org/firefox/)
[![Manifest V2](https://img.shields.io/badge/manifest-v2-blue)](manifest.json)
[![Last commit](https://img.shields.io/github/last-commit/D0n9X1n/humble-apollo)](https://github.com/D0n9X1n/humble-apollo/commits/main)

A dark Firefox theme based on the [Apollo color palette](https://lospec.com/palette-list/apollo)
(46 colors by AdamCYounis).

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
