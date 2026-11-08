# hit-site

The marketing site for **Health Import Tool**, a static page with no build step.

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8765
```

## What is here

| | |
|---|---|
| `index.html` | The whole front page |
| `privacy/` | Privacy policy. The App Store requires a reachable URL for this |
| `support/` | Support page. The App Store requires one of these too |
| `assets/site.css` | All the styling. The palette and the radial lift are the app's own |
| `assets/brands/` | Strava, Garmin, Wahoo, COROS, Suunto, Polar and Zwift logos, and Apple's official App Store badge |
| `screenshots/` | Real screenshots from a real import, not composites. 1020px wide, JPEG. The phone frame round each is drawn in CSS |
| `404.html`, `robots.txt`, `sitemap.xml` | Housekeeping |
| `tools/og-source.html` | Source for the social card. Not served as a page |

## Two things to change before this goes live

1. **`PLACEHOLDER_SUPPORT_EMAIL`** appears in `privacy/index.html` and
   `support/index.html`. The App Store will not accept a privacy policy without
   a way to make contact.
2. **The App Store link** is written out and commented in `index.html`, next to
   the "Coming to the App Store" badge. On approval, swap the badge for the
   link and put the real numeric Apple ID in. Nothing else on the page changes.

## Where it serves

`https://enalmar.github.io/hit-site/`, from `main` at the repository root, the
same arrangement as `gradial-site` and `trackload-site`.

Note the **subpath**. If you later put this on its own domain, as `baton-site`
has, three things change: the canonical tags in the three pages, `sitemap.xml`
and `robots.txt`, and the absolute links in `404.html`. Everything else uses
relative paths and needs no edit.

## About the screenshots

Every one is a real run of HIT 1.0.2 against the reference archive (1,180
files, 133 MB, 1,082 activities once 8 duplicate files are set aside), on an
iPhone 16 Pro Max simulator in dark mode with the status bar set to 9:41. The
Files and Fitness captures are Apple's own apps showing that same import; the
workout opened in Fitness is an indoor Zwift ride, so no real location is
shown. None is a composite. If the app's interface changes, retake them
rather than editing them.

**Never put a bare screenshot on the page.** Every capture goes inside the CSS
phone frame:

```html
<figure class="device">
  <div class="screen"><img src="screenshots/….jpg" width="1020" height="2216" alt="…"></div>
</figure>
```

The frame draws the titanium edge, the bezel, the Dynamic Island and the side
buttons, all as a share of the phone's width, so it holds at any size. The
island is always drawn because simulator captures only sometimes include it.
Add `sm` for the smaller phones in the four-step flow.

Captured at native resolution (1320px wide), then resized **by width** to
1020px and encoded as JPEG at quality 86. 1020px is 3x the largest size a
phone is displayed at, so they stay sharp on a Retina screen. The originals
live outside the repository; `_captures/` is ignored for that reason.

Two traps, both of which caught me:

- `sips -Z` fits the **longest** side. On a portrait screenshot that sets the
  height and leaves the width far too small. Use `sips --resampleWidth`.
- `sips ... --out <same file>` overwrites in place. Keep the natives somewhere
  else, or a second pass has nothing good to work from.

PNG at this size is 500 to 830KB each; JPEG is 60 to 130KB with no visible
artifacts on the dark interface or its small text. Everything below the hero is
`loading="lazy"`, so a first view fetches the two hero phones and nothing else.

## Claims on this page

Everything stated here is either verifiable in the app's repository or was
observed in a run. Specifically:

- **1,082 activities, 1,180 files, 133 MB** is the reference archive, and the
  screenshots show it being read and written.
- **£4.99** is the UK price derived by Apple from the base US price of $4.99,
  checked in App Store Connect on 8 September 2026.
- **100 free** is `FreeAllowance.limit` in the app.
- No speed claim appears anywhere on the page, because no timing has been
  measured on a real iPhone.

Do not add a number here that has not been measured.

## The scroll animation is unverified

Sections fade and lift as they are scrolled to, via `IntersectionObserver` in
`index.html`. **Nobody has watched this work.** Every browser available while
the page was built ran the tab in the background, where Chrome suspends
`requestAnimationFrame` and dispatches no scroll events, so neither the
observer nor any scroll-driven alternative could be made to fire. Open the page
in a normal window and check it before relying on it.

What *is* verified is that the page cannot break because of it:

- The CSS shows every section by default. The script opts into hiding them, and
  only once it knows it can reveal them again. Rendering with JavaScript
  disabled produces a byte-identical page to rendering with it enabled.
- A backstop runs for the first fifteen seconds. If anything more than halfway
  up the viewport is still hidden, the effect is abandoned and every section
  goes back to plainly visible.

If the animation turns out not to fire in real browsers, the page still reads
correctly, which is the property worth protecting.
