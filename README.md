# YapCord for Browser

YapCord is a Vencord-style mod for Yapper: plugins, themes and extra settings on
top of the regular Yapper website. This is the **browser-only** version — no
desktop app, no installer. It comes in two flavours:

- **Chrome extension** — the fuller experience, runs before the page even loads.
- **Bookmarklet** — works in literally any browser, including phone browsers
  like iPhone Safari, no store/extension needed.

You don't need both; pick whichever fits how you browse Yapper.

## Requirements

- **Node.js** 18 or newer ([nodejs.org](https://nodejs.org)) — only needed to *build* either version yourself.
- A Chromium-based browser (Chrome, Edge, Brave, ...) for the extension method.
- Any modern browser (desktop or phone) for the bookmarklet method.

## Get the source

Download this repo's source (zip, or `git clone`) and extract it, then install
dependencies once from inside the extracted folder:

```bash
npm install
```

## Option A — Chrome extension

### Build it

```bash
npm run dist:extension
```

This stages the extension in `dist/extension-stage/` (manifest + icons + the
built `injected.js`). It also writes a ready-to-share zip,
`dist/YapCord-Extension-<version>.zip`.

### Install it (unpacked, for yourself)

1. Open `chrome://extensions` (or `edge://extensions`, etc.).
2. Turn on **Developer mode** (top-right toggle).
3. Click **Load unpacked**.
4. Pick the `dist/extension-stage` folder (not the zip).
5. Go to `yapper.website` (or `yapin.gg`) — YapCord is active. Reload the tab if it was already open.

### Install it on another computer (from the zip)

Send someone `YapCord-Extension-<version>.zip`, have them extract it anywhere,
then follow steps 1-5 above but pick the extracted folder instead.

> This extension is **not published on the Chrome Web Store** — "Load unpacked"
> is the only way to install it, on this computer or any other.

### Updating

Pull/download the newer source, run `npm run dist:extension` again, then on
`chrome://extensions` click the reload icon on the YapCord card (or remove it
and load it unpacked again).

## Option B — Bookmarklet

The bookmarklet needs no build tooling to *use*, but you do need to generate the
install page once:

```bash
npm run dist:bookmarklet
```

This writes `dist/YapCord-Bookmarklet.html`. Open that file in a browser and
follow the instructions on the page — it covers:

- **Desktop**: drag the "Install YapCord" button straight to your bookmarks bar.
- **iPhone**: the Shortcuts-app method (works fully on Safari, where regular
  bookmarklets are otherwise awkward to run).
- **Any phone**: create the bookmark on a synced desktop browser and let it sync over.

Once installed, tap/click the bookmark while you're on `yapper.website` to turn
YapCord on for that tab. You need to do this once per visit/reload — it isn't
permanent like the extension.

### Good to know

- It runs *after* the page has already loaded, so the very first requests of a
  fresh page load aren't covered by NoTrack — everything else (Plugins page,
  themes, Custom CSS, the rest of the plugins) behaves the same either way.
- Tapping it again on an already-loaded tab is harmless.
- Settings are stored in that browser's own `localStorage` for `yapper.website`,
  separate from the desktop app and the extension.

### Updating

Re-run `npm run dist:bookmarklet`, open the new `dist/YapCord-Bookmarklet.html`,
and re-install the bookmark the same way — the old one keeps pointing at the old
code until you replace it.

## Troubleshooting

| Problem | Fix |
|---|---|
| `chrome://extensions` shows an error after "Load unpacked" | Make sure you picked the `dist/extension-stage` folder itself, not its parent or the zip. |
| Nothing happens after loading the extension | Reload the `yapper.website`/`yapin.gg` tab — it only takes effect on page load. |
| The bookmarklet does nothing on iPhone | A plain bookmarklet link often just "runs" once on tap instead of saving — use the Shortcuts-app method described on the install page instead. |
| `npm run dist:extension` / `dist:bookmarklet` fails | Run `npm install` first if you haven't, and make sure you're in the folder that directly contains `package.json`. |

## Which one should I use?

| | Extension | Bookmarklet |
|---|---|---|
| Needs install per visit | No — stays on | Yes — tap/click each time |
| Works on iPhone | No (no Chrome extensions on iOS) | Yes |
| Runs before page load (catches the very first requests) | Yes | No |
| Setup | Developer mode + Load unpacked | One tap once installed |
