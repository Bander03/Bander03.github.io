# Hardening Review — Week 9 ("Break Your Own Site")

## How this was tested

Real testing against the live site (`bander03.github.io`), not assumptions:
- Contact form: submitted empty, submitted with garbage/XSS-attempt input, submitted with an
  invalid email format, and stress-tested with a rapid double-click — instrumented with a
  fetch-call counter (mocked network, then re-tested with a realistic 400ms delay) to get a
  real yes/no answer instead of guessing from the UI alone.
- Every link on the page checked by loading it (`curl -L -w "%{http_code}"`), not eyeballed.
- SEO and performance: real Google PageSpeed Insights (Lighthouse) run against the live URL.
- Findability: real web searches for my own name and `site:bander03.github.io`.

## Findings, sorted: fix-now vs. known limitation

### Fix-now (all fixed today, on the live site)

| # | Finding | Evidence | Fix |
|---|---|---|---|
| 1 | **Double-click on the contact form sends the message twice.** Instrumented test confirmed `fetchCount: 2` on a double-click with a realistic network delay. | Real bug, not hypothetical — a mocked instant-response test first hid it; retesting with a realistic 400ms delay reproduced it reliably. | Added a `sending` guard flag + `submitBtn.disabled = true` for the duration of the request. Re-tested: `fetchCount: 1`. |
| 2 | **No meta description.** Lighthouse SEO score: 91/100, single failing audit: "Document does not have a meta description." | Confirmed via PageSpeed Insights live run. | Added `<meta name="description">`. |
| 3 | **No social-share preview (Open Graph / Twitter Card).** Pasting the link into Slack/X/LinkedIn would show a bare link, no title, no image. | Manually confirmed absent from `<head>`. | Added `og:title`, `og:description`, `og:image` (new branded 1200×630 `assets/og-image.png`), `og:url`, and matching `twitter:card` tags. |
| 4 | **Chart and logo `<img>` tags have no explicit width/height.** Lighthouse diagnostic: "Image elements do not have explicit width and height" — a real layout-shift risk on slow connections. | Confirmed via PageSpeed Insights diagnostics. | Added `width`/`height` attributes to all three `<img>` tags (CSS still controls final rendered size; these just reserve space before it loads). |
| 5 | **No `<main>` landmark.** Lighthouse Best Practices: "Document does not have a main landmark." | Confirmed via PageSpeed Insights. | Wrapped all page content (hero through the contact form) in `<main>`. |
| 6 | **No `robots.txt` / `sitemap.xml`.** Basic crawlability hygiene missing entirely. | Confirmed absent (404 on both paths). | Added minimal `robots.txt` (allow all) and a one-URL `sitemap.xml`. |

### Verified working, no fix needed

- **Empty form submission:** correctly blocked by the browser's native `required` validation —
  no crash, no bad request sent.
- **Garbage/XSS input** (`<script>alert(1)</script>`, a SQL-injection-style string, emoji, a
  200+ character name): stored as inert text in the input value, never executed — this is
  expected, safe default behavior for form fields, not a vulnerability.
- **Invalid email format** (`not-an-email`): correctly blocked by `type="email"` native
  validation.
- **All 7 outbound links** (GitHub repo ×2, GitHub profile, LinkedIn, model report, capstone
  spec, workflows folder): every one returns 200, checked by loading it, not by reading the href.

### Known limitations (named, not hidden)

- **The live site isn't indexed by Google yet.** Searching my own name and `site:bander03.github.io`
  surfaced the GitHub *repository* pages, but not the rendered site itself. This is expected —
  the site is only days old, and search engines take time to crawl and index a new domain even
  with correct meta tags in place. The meta/robots/sitemap fixes above are the addressable part
  (making the site *legible* once crawled); the crawl delay itself isn't something a same-day
  fix can solve. Next step if this doesn't resolve on its own: submit the URL directly via
  Google Search Console.
- **Render-blocking Google Fonts request, ~2,070ms estimated savings per Lighthouse.** Real, and
  the single biggest lever left on the Performance score (currently 90/100 — already in the
  "good" tier). Fixing it well means either self-hosting the fonts or loading them
  asynchronously via JS, both of which trade a meaningful amount of new complexity (self-hosting:
  a font-serving pipeline; async loading: real risk of a flash of unstyled text) for a score
  that's already comfortably in the green. Documenting as accepted, not silently dropped.
- **Not tested on a literal physical phone**, per the Week 7 fix log's same caveat — extensive
  real mobile-viewport emulation was done, but a genuine "opened it on my actual phone" pass is
  still worth 30 seconds whenever convenient.

## Real Lighthouse scores (live URL, mobile, slow-4G throttled)

| Category | Score |
|---|---|
| Performance | 90 |
| Accessibility | 97 |
| Best Practices | 100 |
| SEO | 91 → (91 was pre-fix; meta description now added) |

## Hardening review

*(To be completed: send this document + the live URL to a mentor or the same structured peer
reviewer as Week 7, specifically asking them to try to break it — not just react to it. Log
their findings and fixes here once received.)*
