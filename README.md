# MyKK HTML Viewer

A fast, mobile-first, **single-file** HTML viewer. Drag & drop an HTML file
(or any text file) anywhere on the page: HTML **renders** instantly, and one
tap flips to a syntax-highlighted **code view**. CSS, SCSS, JS, JSON, YAML,
Markdown, `.txt` — any text file — open straight into the highlighted source.
It's a **viewer, not an editor** — no toolbars, no accounts, no uploads.
Everything runs locally in your browser.

🔗 **Live:** <https://html-viewer.us/>

![Single file](https://img.shields.io/badge/build-single%20HTML%20file-success) ![No build step](https://img.shields.io/badge/build%20step-none-success) ![License](https://img.shields.io/badge/license-MIT-blue)

## Features

- 🖥️ **Renders HTML** — drop an `.html`/`.htm`/`.svg` file and it renders in a
  **sandboxed iframe**, faithfully — its own inline CSS, images, and web fonts
  included.
- `</>` **Code view** — a toggle button flips between the rendered page and the
  **syntax-highlighted source**, with line numbers.
- 📄 **Any text file** — `.css`, `.scss`, `.less`, `.js`, `.ts`, `.json`,
  `.yaml`, `.md`, `.xml`, `.py`, `.sql`, `.sh`, `.txt`, and
  [many more](#supported-file-types) open directly into the highlighted source.
- 🏷️ **Filename in the header** — when you open or drop a file, its name shows
  in the top-left.
- ➕ **New** (`+`) — clears the screen and opens a file picker.
- 📋 **Copy** — copies the raw source to your clipboard.
- 🗑️ **Clear** — empties the view.
- 🎨 **Pick any background color** — a color swatch in the header lets you choose
  any background. Text, borders, and syntax colors automatically adapt for
  contrast. Your choice is **remembered** — saved to a cookie, with a
  `localStorage` fallback so even a downloaded `file://` copy remembers it.
  Starts on white.
- 🫥 **Distraction-free** — once a file is loaded the header slides away; move
  your mouse to the **top of the window** (or tap the top edge on mobile) to
  bring it back.
- 📱 **Mobile-first** & responsive, with safe-area support for notched phones.
- 🔒 **Safe by default** — HTML is rendered inside a locked-down `sandbox`
  iframe, so **scripts never run** and a malicious file can't touch the page or
  your data. Your files never leave your device.
- 🪶 **One file, no build** — `index.html` is self-contained (~150 KB) and the
  viewer works offline, even straight from `file://`.
- 📊 **Privacy-friendly analytics** — the hosted site uses a self-hosted,
  cookieless [Plausible](https://plausible.io/) instance (see [Privacy](#privacy)).

## Quick start

**Just open it.** Download [`index.html`](index.html), double-click it, and
you're done — it runs locally with no server, no build, and no internet
connection.

Prefer a local server?

```sh
python3 -m http.server 8080   # then open http://localhost:8080
```

Any static web server works too — there is nothing to build.

## Supported file types

**Rendered as a page** (with a toggle to source): `.html`, `.htm`, `.xhtml`,
`.shtml`, `.svg`. A file with no extension is rendered too when its content
starts with `<!doctype html>`, `<html>`, or `<svg>`.

**Opened as highlighted source:** `.css` · `.scss` · `.sass` · `.less` ·
`.js` · `.mjs` · `.jsx` · `.ts` · `.tsx` · `.json` · `.json5` · `.xml` ·
`.yaml`/`.yml` · `.toml`/`.ini` · `.md` · `.py` · `.rb` · `.php` · `.java` ·
`.c`/`.h` · `.cpp` · `.cs` · `.go` · `.rs` · `.kt` · `.swift` · `.sql` ·
`.sh`/`.bash` · `.pl` · `.lua` · `.r` · `.graphql` · `.diff`/`.patch` ·
`makefile` · `.txt` · `.log` · `.csv` — and anything else drops in as plain
text. The language is picked from the extension, falling back to
automatic detection.

## Deploy to Cloudflare Pages (auto-deploy from this repo)

Connect the repository in the Cloudflare dashboard
(**Workers & Pages → Create → Pages → Connect to Git**) and use:

| Setting                  | Value            |
| ------------------------ | ---------------- |
| Production branch        | `main`           |
| Framework preset         | `None`           |
| Build command            | *(leave blank)*  |
| Build output directory   | `/`              |

It's a static site — Cloudflare just serves `index.html`. The included
[`_headers`](_headers) file applies security headers (CSP, `nosniff`,
`frame-ancestors`, etc.) automatically. Every push to `main` then
auto-deploys.

Add your custom domain `html-viewer.us` under the project's **Custom domains**
tab — Cloudflare creates the DNS record and provisions SSL for you.

## How it works

Everything is in [`index.html`](index.html):

- Your HTML/CSS/UI and the app logic — no build step, no tooling.
- HTML is written to a **`sandbox`ed `<iframe>`** via `srcdoc`. The sandbox has
  no `allow-scripts`, so the rendered page displays with its own styles but
  **cannot execute any JavaScript** — that's the security boundary.
- [**highlight.js**](https://github.com/highlightjs/highlight.js) `v11.9.0`
  (BSD-3-Clause) powers the code view, embedded inline (minified, with its
  license banner retained), so highlighting works with **no network
  dependencies** and fully offline. The only external request is the analytics
  script on the hosted site (see [Privacy](#privacy)).

## Privacy

Your files stay on your device — they're read in the browser and never uploaded
anywhere, and your content is never sent to any server.

The hosted site at **html-viewer.us** uses a self-hosted
[Plausible](https://plausible.io/) instance for **privacy-friendly, cookieless**
page analytics: aggregate visit counts only — no personal data, no cross-site
tracking, no advertising. Plausible automatically ignores `localhost` and
`file://`, so a downloaded local copy reports nothing.

The only thing stored on your device is your chosen background color (a cookie,
with a `localStorage` fallback).

## License

[MIT](LICENSE) © 2026 Michal Ferber, aka **TechGuyWithABeard**.

The bundled third-party library retains its own license (highlight.js:
BSD-3-Clause) — see [`LICENSE`](LICENSE) for details.
