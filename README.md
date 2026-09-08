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
| `screenshots/` | Real screenshots from a real import, not mockups |
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

Every one is a real run against the real 1,090-activity reference archive, not
a mockup and not a composite. If the app's interface changes, retake them
rather than editing them.

## Claims on this page

Everything stated here is either verifiable in the app's repository or was
observed in a run. Specifically:

- **1,090 activities, 133 MB** is the reference archive, and the screenshots
  show it being read.
- **£4.99** is the UK price derived by Apple from the base US price of $4.99,
  checked in App Store Connect on 8 September 2026.
- **100 free** is `FreeAllowance.limit` in the app.
- No speed claim appears anywhere on the page, because no timing has been
  measured on a real iPhone.

Do not add a number here that has not been measured.
