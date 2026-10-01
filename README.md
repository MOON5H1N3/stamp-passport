# Stamp Passport

A digital stamp passport for heritage places. Visit somewhere, tap it, and it gets an inked stamp with the date and a note.

- **133 places** across England, Wales and Northern Ireland, grouped by region, each with its own illustrated stamp
- **Add your own places** if one is missing
- **Works offline** once it has been opened, so it is fine at places with no signal
- **Installs like an app** from the browser, with its own home-screen icon
- **Private:** stamps are saved on your device only. There are no accounts and no server
- **Backup and restore** your stamps as a small JSON file, e.g. when changing phone

An unofficial personal record, not affiliated with the National Trust. The stamp illustrations are original drawings.

## Installing on a phone

- **iPhone / iPad:** open the link in Safari, tap Share, then **Add to Home Screen**.
- **Android:** open the link in Chrome and tap **Install app** at the bottom of the page, or use the ⋮ menu → **Install app**.

## How it is built

Plain static files with no build step and no dependencies:

| File | What it does |
| --- | --- |
| `index.html` | The whole app: place list, stamp drawings (generated SVG), storage, backup |
| `manifest.webmanifest` | Name, colours and icons for installing |
| `sw.js` | Service worker that caches the app and fonts for offline use |
| `icons/` | App icons |

Stamps live in the browser's `localStorage` under the key `heritage-passport-v1`.

## Hosting

Serve the folder from any static host. All paths are relative, so it also works from a subfolder such as `/stamp-passport/`. Keep the trailing slash in links to it.

**Cloudflare Workers with static assets:** put this repo's files in a `stamp-passport/` folder inside the site's assets directory, then `npx wrangler deploy`.

**Cloudflare Pages / Netlify / GitHub Pages:** deploy the repo root as-is.

## Releasing an update

1. Edit the files.
2. Change `VERSION` at the top of `sw.js` (e.g. `passport-v2`), so installed copies pick up the new version.
3. Deploy. Phones get the update the next time the app is opened.

Adding a place to the built-in list: add an entry to the right region in the `RAW` table in `index.html`, in the form `Name~Short label|type|motif options`. The short label is optional and is used on the stamp when the full name is long.

## License

MIT
