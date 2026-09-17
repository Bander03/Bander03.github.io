# Run 6 — "Brand new input" generalization test (not one of the 5 scored runs)

**Topic (chosen after the pipeline and the 5 runs above were already finished, specifically to
test generalization):** "Core Web Vitals ranking factor changes, 2026"

## Step 1 — Gather

- [Core Web Vitals 2026: What Changed — Hyperspeed](https://hyperspeed.me/blog/core-web-vitals-2026-what-changed/)
- [How important are Core Web Vitals for SEO in 2026? — White Label Coders](https://whitelabelcoders.com/blog/how-important-are-core-web-vitals-for-seo-in-2026/)
- [Core Web Vitals 2026: Technical SEO That Actually Moves the Needle — ALM Corp](https://almcorp.com/blog/core-web-vitals-2026-technical-seo-guide/)
- [Core Web Vitals in 2026: What's Changed & What Still Matters — Upward Engine](https://upwardengine.com/blog/core-web-vitals-2026/)
- [The Most Important Core Web Vitals Metrics in 2026 — Nitropack](https://nitropack.io/blog/most-important-core-web-vitals-metrics/)

## Step 2 — Synthesize

- INP (Interaction to Next Paint) has fully replaced FID, now measuring every interaction across
  a session, not just the first click. (Multiple sources, consistent — consensus)
- A new metric, VSI (visual stability, session-wide), is reported as introduced in 2026.
  (Single source for the specific "VSI" name — flag)
- Google's reported March 2026 core update rolled LCP/INP/CLS into a composite score that sits
  *alongside* content signals rather than behind them. (Single source for this specific framing)
- Repeated framing across sources: Core Web Vitals remain a **tie-breaker**, not the deciding
  factor — content quality and E-E-A-T still come first; CWV decides between pages that are
  otherwise similar in content quality.

## Step 3 — Draft

# Core Web Vitals — Weekly Brief
**Why it matters:** page speed still doesn't outrank good content — but it increasingly decides ties, and the metrics being measured changed.
- INP (Interaction to Next Paint) has fully replaced FID as the responsiveness metric, now scoring every interaction in a session rather than just the first one.
- One source reports a new 2026 metric, VSI, measuring visual stability across the whole session rather than only initial page load — treat this as an emerging, not yet widely confirmed, addition.
- Core Web Vitals are consistently described as a tie-breaker: when two pages are similar in content quality, the faster/more stable one reportedly wins; content and E-E-A-T still come first.
**Watch next:** whether "VSI" shows up as a named metric in your own Search Console / PageSpeed Insights reporting, since this run found it in only one source.

## Step 4 — Review (self-critique)

- Every bullet traces to a named source. ✔
- The "VSI" metric claim is the single-source item in this run — correctly hedged as
  "one source reports... not yet widely confirmed" rather than stated as settled fact. ✔
- The tie-breaker framing is corroborated across sources — left unhedged. ✔
- No forbidden absolute language. ✔

## Step 5 — Final brief

# Core Web Vitals — Weekly Brief
**Why it matters:** page speed still doesn't outrank good content — but it increasingly decides ties, and what's being measured changed.
- INP (Interaction to Next Paint) has fully replaced FID as the responsiveness metric, now scoring every interaction in a session rather than just the first one.
- One source reports a new 2026 metric, VSI, measuring visual stability across the whole session rather than only initial page load — an emerging addition this run found in only one source, not yet widely confirmed.
- Core Web Vitals are consistently described as a tie-breaker: when two pages are similar in content quality, the faster/more stable one reportedly wins — content quality and E-E-A-T still come first.

**Watch next:** whether "VSI" shows up as a named metric in your own Search Console / PageSpeed Insights reporting.

**Sources:**
- [Hyperspeed — Core Web Vitals 2026: What Changed](https://hyperspeed.me/blog/core-web-vitals-2026-what-changed/)
- [White Label Coders — How important are Core Web Vitals for SEO in 2026?](https://whitelabelcoders.com/blog/how-important-are-core-web-vitals-for-seo-in-2026/)
- [Nitropack — The Most Important Core Web Vitals Metrics in 2026](https://nitropack.io/blog/most-important-core-web-vitals-metrics/)

**Human should still check:** the "VSI" metric name — single-sourced in this run, worth confirming against Google's own web.dev documentation before using the term in client materials.

## Result of this generalization test

The pipeline ran start to finish on a topic that did not exist anywhere in the pipeline's
design or in the 5 scored runs above, using the same fixed 5-step instructions, with no manual
adjustment. It produced the same shape of output (gather → tagged synthesis → drafted brief →
self-critique with at least one flagged single-source claim → final under-300-word brief with a
named human-check item). That's the "runs end to end on a brand new input" criterion, satisfied
by construction rather than by re-running an input the pipeline was tuned against.
