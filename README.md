# RockSteady — Vintage National-Park (multipage build)

A full **multipage** static build of the RockSteady site in the **Vintage National-Park**
design direction (Direction B from the design review). It preserves the navigation and
page organization of the current production site at
[rocksteady-fitness.com](https://rocksteady-fitness.com), and every subpage's copy is
reproduced **verbatim** from the current production pages.

## Structure

```
vintage-preview/
├── index.html            # Home (un-bundled from the vintage-park preview)
├── pages/
│   ├── about.html
│   ├── guide.html        # App Guide (quick guide)
│   ├── user-guide.html   # complete User Guide (full reference)
│   ├── contact.html      # contact form re-implemented in vanilla JS
│   ├── privacy.html
│   └── terms.html
├── css/
│   └── site.css          # shared vintage design system (all pages link this)
└── assets/
    ├── fonts/            # self-hosted Bricolage Grotesque + Space Mono (OFL 1.1)
    └── img/              # decoded from the vintage-park asset bundle
        └── spare/        # unused-but-kept imagery (not referenced by any page)
```

## Navigation & organization (matches production)

- **Header:** Home · About · Guide · Privacy · Contact  +  "Get the app"
- **Footer — Pages:** Home · About · App Guide
- **Footer — Legal:** Privacy Policy · Terms of Service · Contact

Terms of Service lives in the footer only (no top-nav link), same as production.
Mobile (≤900px) uses a CSS-only hamburger menu (no JS); the "Get the app" pill moves inside it.

## Home page (section order)

1. **Hero** — "Push your rock. Stay steady." + App Store badge
2. **Stamp strip** — Strength · Cardio · Recovery · Sport · On-device
3. **Privacy — "Leave no trace."** — promoted no-data-collection statement (0 trackers · 100% on
   your device), placed high, before features/screenshots
4. **Photo band** — climbing (Fig. 01)
5. **Discipline emblems** — the four sloth mascots, as a visual intro to the disciplines
6. **Field Guide** — detailed discipline entries with app screenshots
7. **Apple Watch** → **Feature cards** (Sports / Calendar / Social)
8. **Photo band** — lakefront (Fig. 02) → **Philosophy** quote → **CTA** → footer

Home-only additions beyond the raw vintage-park preview: the promoted privacy band, two
full-bleed photo bands (real photography), the emblems repositioned as the disciplines intro
(overview → detail), and the responsive hamburger nav.

## Design system

- **Fonts:** **Bricolage Grotesque** (display/body) + **Space Mono** (labels), **self-hosted**
  from `assets/fonts/` (SIL OFL 1.1 — see `assets/fonts/LICENSES.md`). No Google Fonts CDN, so
  no visitor IP is sent to Google.
- **Palette:** cream paper `#EFE6D2`, ink `#3A2E1F`, moss `#3A5A3C`, ochre/gold `#CB8B2E`,
  rust `#A8431E`, brown `#4A3826`. Hairline dashed rules and hard offset shadows.
- Fully static and self-contained — no external CDN calls (only the App Store deep-links).

## Copy provenance

Home copy is the approved vintage-park redesign copy. All six subpages
(`about`, `guide`, `user-guide`, `contact`, `privacy`, `terms`) carry the **exact** text of
the corresponding production pages — verified string-for-string against
`rocksteady-fitness-website/pages/*.html`. No wording was changed, added, or removed.

## Preview / launch

Deployed for preview via GitHub Pages at **https://doc-rode.github.io/vintage-preview/**
(public repo `doc-rode/vintage-preview`). `.nojekyll` serves the files as-is.

Kept out of search two ways:
1. A `noindex, nofollow` `<meta>` on **every page** — the effective control for a
   `github.io/<repo>/` project-page URL.
2. An authoritative `robots.txt` at the **account root** —
   `doc-rode.github.io/robots.txt` (repo `doc-rode/doc-rode.github.io`) — with
   `Disallow: /vintage-preview/`. (A `robots.txt` inside this repo would sit at a subpath and be
   ignored by crawlers, so it lives at the domain root instead.)

> **Before launch:** every page carries `<meta name="robots" content="noindex, nofollow">`
> (marked `PREVIEW ONLY: remove at launch`). **Remove these tags at production** so the real
> site can be indexed (and drop the root `Disallow` if the launch URL stays under
> `doc-rode.github.io`).

## Known follow-ups (not copy changes)

- **`user-guide.html`** is a **generated** page in production (built from `docs/User-Guide.md`
  via `scripts/build-guide.py`). It has been ported here as a static vintage page with the
  body copy verbatim. If the Markdown source changes, this page must be regenerated/re-skinned
  to match (the build script's template still emits the old slate-blue design).
- **App Store badge** — CTAs now use the official **"Download on the App Store"** badge
  layout (`assets/img/appstore-badge-black.svg` on light sections, `-white.svg` on the dark
  rust CTA bands) instead of a custom Apple-logo button, per Apple's marketing guidelines.
  These SVGs are faithful reproductions of Apple's badge; for full compliance, replace the two
  files in-place with Apple's official downloaded artwork (same filenames — drop-in swap). The
  header "Get the app" link is plain text (no Apple logo), which is allowed. **This is also a
  fix worth applying to the production site**, which still uses the custom Apple-logo button.
- **Home photography** — two full-bleed human photos (`assets/img/photo-climbing.jpg`,
  `photo-lakefront-rest.jpg`) put a human face on the app. They are **AI-generated placeholders**
  (so there's no third-party stock license to clear) — optimized to ~200–260 KB JPEGs. Before
  launch: (1) eyeball them at full size for AI artifacts (hands/feet/watches), and (2) plan to
  **swap in authentic photos of real users/locations** when available — the strongest
  "a human made this" signal.
- **Contact form** has no backend (mirrors production): it validates and shows the
  "Message sent" confirmation client-side only. Wire to a real handler before launch.
- Guide/how-to screenshots that didn't exist in the vintage asset bundle are shown as
  vintage placeholder panels (play badge + duration); no images were invented.
