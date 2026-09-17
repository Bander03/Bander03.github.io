# Identity Kit

## Style note (two lines)

Serif headings (Lora) over clean sans body text (Inter), on a near-white ground with one
confident blue accent — quiet and legible, like a well-kept research notebook, not a startup
landing page.

## Fonts

- **Heading:** [Lora](https://fonts.google.com/specimen/Lora) — free Google Font, serif, used
  for `h1`/`h2` only
- **Body:** [Inter](https://fonts.google.com/specimen/Inter) — free Google Font, sans, used for
  everything else (paragraphs, nav, buttons, labels)

Two fonts, no more. Both load from Google Fonts CDN in `index.html`.

## Palette (3 colors, one accent)

| Role | Hex | Use |
|---|---|---|
| Background (near-white) | `#F7F8FA` | Page background |
| Text (near-black) | `#14181F` | Body copy, headings |
| Accent (the one color) | `#1A52B0` | Links, CTA buttons, section labels, logo |
| Accent tint (derived, not a second color) | `#E7EEFB` | Card backgrounds only — a lighter tint of the accent, not an independent hue |

This carries forward the blue already used in the FL-02 prompt-iteration log (`done.html`), so
the two deliverables read as the same person's work instead of two unrelated styles.

## Logo / favicon

A simple text wordmark — initials **BS** set in Lora, white text inside a solid accent-blue
circle. No external image-generation needed: it's an inline SVG (`assets/logo.svg`,
`assets/favicon.svg`), so it renders crisp at any size and costs nothing to change later.

## Consistency rule applied across the site

- Only the accent color is ever used for anything clickable — no second "cheerful" color, no
  gradient, no multi-color badge system.
- No drop shadows beyond one subtle card shadow; no background imagery behind text.
- Charts keep their own report styling (teal bars, white background) — they are *proof*, not
  decoration, so they're framed in a plain card rather than restyled to match the palette. Forcing
  chart colors to match the brand would blur the line between "real result" and "decoration,"
  which is the mistake this whole exercise is about avoiding.
