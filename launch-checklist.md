# Launch Checklist — Week 9 ("Plant Your Flag")

## 1. Custom domain

**Decision: keep `bander03.github.io`** — the free fallback, not a purchased domain. Consistent
with the Week 4 stack decision (`stack-decision.md`): free-only, matched to real need. Already
live, already HTTPS, no new infrastructure. Revisit if a paid domain becomes worth it later —
nothing here is locked in.

## 2. Analytics

**Cloudflare Web Analytics**, installed via a `<script>` beacon in `<head>` — no cookies, no
consent banner needed (Cloudflare's analytics are cookie-less by design), genuinely free.
Verified locally before deploying: the script tag is present with the correct site token and
loads with zero console errors.

*(Screenshot evidence: once traffic has hit the live site for a few minutes, open the Cloudflare
dashboard → Web Analytics → bander03.github.io and screenshot the live numbers — that's the
actual required proof and has to come from your own dashboard login, not something I can capture.)*

## 3. Launch hygiene — verified on the real live address

- **HTTPS:** confirmed — `https://bander03.github.io/` returns 200 over TLS.
- **Page title:** confirmed correct in the browser tab — "Bander Sidiq — Applied ML for Search".
- **Favicon:** confirmed loading — `assets/favicon.svg` returns 200.
- **Social-share preview:** confirmed — `og:title`, `og:description`, `og:image` all present and
  `assets/og-image.png` (the branded 1200×630 card added in Week 9's hardening pass) returns 200.
- **Opened on a real phone:** same honest caveat as Weeks 7 and 9's hardening pass — extensively
  verified via mobile-viewport emulation, but a literal physical-phone open is still worth the
  30 seconds whenever you have a spare moment.

## 4. FlyRank graduate badge — blocked, not faked

**Status: cannot be installed yet.** The badge generator at
[internship-badge.netlify.app](https://internship-badge.netlify.app/) requires a real Credential
ID, which FlyRank issues **after capstone approval** — per the FL-06 assignment's own text:
"Instructions and the badge asset will be provided when your capstone is approved. There is
nothing you need to request or configure now." That hasn't happened yet.

**What I did instead of faking it:** left an HTML comment in the footer marking exactly where
the badge snippet goes, and deliberately did **not** add a visible "badge coming soon" placeholder
pill to the live page — Week 7's design crit specifically flagged a dead "CV (add link)" pill as
the single most credibility-damaging thing on the site, and repeating that pattern here would be
the same mistake.

**To finish this step once the credential exists:**
1. Go to [internship-badge.netlify.app](https://internship-badge.netlify.app/), enter the real
   Credential ID, first name, track (Machine Learning), and cohort.
2. Pick a shape (a "Chip" or "Line" badge fits the current minimal footer best).
3. Copy the HTML snippet and paste it into `index.html`'s footer, replacing the placeholder
   comment.
4. Commit, push, and confirm the badge is visible and its verify link resolves.

## What to submit now vs. after the badge exists

This checkpoint's other three requirements (domain, analytics, launch hygiene) are complete and
live today. The badge requirement is genuinely blocked on FlyRank's side, not on unfinished work
here — flag that honestly on submission rather than waiting silently or shipping a fake badge.
