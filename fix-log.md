# Fix Log — Mobile Polish Pass (Week 7, "Open It On Your Phone")

Audit method: real mobile emulation (375×812), tablet (768×1024), and desktop widths in a live
browser session on the actual deployed URL (`bander03.github.io`) — not just a resized desktop
window. Contrast ratios computed with the actual WCAG formula against the site's real CSS
variables. Every link tested by loading it, not just eyeballing the href.

## What was broken

### 1. Chart text unreadable at every width, worst on mobile (readability)
The two case-study charts are 960px-wide SVGs. The CSS scaled them to `width: 100%` of their
card, which on a stacked mobile column (~340px) shrank the chart to about a third of its native
size — bar labels like `days_with_impressions` and value numbers became genuinely hard to read,
not just small. This wasn't mobile-only: even on desktop's 2-column grid, cards are ~400px wide,
still well under the chart's native 960px, so the same problem existed everywhere, just less
severely.
**Fix:** charts now render at a legible minimum width (480px) inside a horizontally-scrollable
card (`overflow-x: auto`), with a "Scroll to see the full chart →" hint that only shows on
narrow screens. Text is crisp at every width now; narrow viewports scroll instead of squinting.

### 2. Tap targets below the 44px minimum (mobile usability)
Measured actual rendered heights on the live site:
- Hero pills (LinkedIn / GitHub / CV / Book a time): **37px**
- "Read the full model report →" link: **19px**
- Footer links (LinkedIn / GitHub / Email): **17px**

All below the widely-used 44px minimum recommended tap-target size (Apple HIG / WCAG 2.5.5) —
on a real phone these are genuinely fiddly to tap accurately, especially the footer, where three
links sit close together separated only by a middle dot.
**Fix:** added `min-height: 44px` with flex centering to `.pill`, `.secondary-cta`, and
`footer a`. Visual size barely changed — the extra tap area is mostly invisible padding, not a
bigger-looking button.

## What was checked and passed (no fix needed)

- **Color contrast:** computed WCAG contrast ratios for every text/background pair actually used
  (muted text on background: 6.01:1, muted on card surface: 6.39:1, body text: 16.75:1, button
  text on accent: 7.30:1, links on background: 6.87:1). WCAG AA requires 4.5:1 for normal text —
  every pair clears it comfortably.
- **Every link on the page**, checked by loading it (not just visually): the GitHub repo link,
  the model report link, the two capstone/workflow links, and the GitHub profile link all return
  200. The LinkedIn profile link initially looked broken to an automated `curl` check (LinkedIn
  returns a bot-blocking response to non-browser requests) — verified as a false alarm by loading
  it in an actual browser, where it resolves correctly to the real profile.
- **Image size:** all chart assets are SVGs (1–4 KB each) — no oversized raster images to
  compress.
- **Layout at tablet and desktop widths:** no broken grids, no overflow, no clipped text found at
  either width.

## Before / after

| | Before | After |
|---|---|---|
| Chart label text on mobile | Squeezed to ~340px, hard to read | Renders at 480px min-width, crisp, with a scroll hint |
| Hero pill tap height | 37px | 44px |
| Footer link tap height | 17px | 44px |
| "Read the full model report" tap height | 19px | 44px |
| Contrast | Already passing | Unchanged — verified, not assumed |
| Links | 1 false-alarm (LinkedIn, bot-blocked curl) | Verified all real in an actual browser |

Live URL after fixes: **https://bander03.github.io/**
