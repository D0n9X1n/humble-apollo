# Humble Apollo — Firefox Theme

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

## Releasing a new version to Firefox (AMO)

Themes are distributed through [addons.mozilla.org](https://addons.mozilla.org) (AMO). Firefox only
installs permanently-signed add-ons, and **AMO is the signer**.

1. **Bump the version** in both `manifest.json` (`version`) and `package.json` (`version`). AMO
   rejects re-uploading a version that already exists.
2. **Build**: `npm run build` → `web-ext-artifacts/humble_apollo-<version>.zip`.
3. **Submit** the `.zip`:
   - **First release** — sign in at <https://addons.mozilla.org/developers/>, click *Submit a New
     Add-on*, upload the zip, choose **listed** (public on AMO) or **unlisted** (self-distributed
     `.xpi` you host yourself), and fill in the listing (name, summary, screenshots, categories).
   - **Update** — open the add-on → *Manage* → *Upload New Version* → upload the new zip.
   - **CLI alternative** — generate API credentials at
     <https://addons.mozilla.org/developers/addon/api/key/> and run:
     ```sh
     npx web-ext sign --channel listed \
       --api-key "$AMO_JWT_ISSUER" --api-secret "$AMO_JWT_SECRET"
     ```
     `--channel listed` publishes on AMO; `--channel unlisted` returns a signed `.xpi` for
     self-hosting.
4. **Review** — listed submissions go through Mozilla review (themes are usually fast/automated).
   Once approved it's live at `addons.mozilla.org/firefox/addon/humble-apollo/`.

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
