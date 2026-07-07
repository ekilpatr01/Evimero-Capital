---
name: preview
description: Serve and visually preview the Evimero Capital site (index.html) locally, and optionally screenshot it. Use whenever you edit index.html and want to confirm the change renders correctly before committing, or when the user asks to "preview", "see", "run", or "screenshot" the site.
---

# Preview the Evimero Capital site

The repo is a single static file, `index.html`. There is no build step. To view a change, serve the repo root over HTTP (opening the file directly with `file://` breaks the Google Fonts `preconnect` and some relative behavior).

## Serve it

Start a local server from the repo root:

```bash
python3 -m http.server 8000
```

Then the site is at `http://localhost:8000/`. Run the server in the background so you can keep working, and stop it when done.

## Screenshot it (to actually verify a change)

Chromium + Playwright are available in this environment. Capture the full page and key breakpoints so you can see the result rather than guessing:

```bash
python3 - <<'PY'
from playwright.sync_api import sync_playwright
URL = "http://localhost:8000/"
shots = [("desktop", 1440, 900), ("mobile", 390, 844)]
with sync_playwright() as p:
    b = p.chromium.launch()
    for name, w, h in shots:
        pg = b.new_page(viewport={"width": w, "height": h})
        pg.goto(URL, wait_until="networkidle")
        pg.wait_for_timeout(800)  # let scroll-reveal animations settle
        pg.screenshot(path=f"/tmp/evmc-{name}.png", full_page=True)
    b.close()
print("done")
PY
```

Then Read the PNGs and send them to the user with SendUserFile so they can see it too.

## What to check after an edit

- The hero, about, services, stats, and contact sections all render and are in order.
- `reveal` scroll animations don't leave content stuck invisible (elements start at `opacity:0` and reveal on scroll — if JS breaks, content stays blank).
- Both **desktop and mobile** layouts (there's a mobile nav breakpoint around the `--nav-h` change).
- Google Fonts (Playfair Display serif, Lato sans) load — if they don't, headings fall back to Georgia.
