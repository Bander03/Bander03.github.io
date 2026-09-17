# Explain It Like You Built It — CSS variables

**The piece of my build:** the `--accent` CSS custom property in [index.html](index.html), and
how one variable controls color across the whole page.

**My explanation, in my own words:**

In my portfolio's CSS, there's a line near the top that says `--accent: #1A52B0`. That's a
variable — basically a name I can attach to a color instead of typing the color out every time.
All over the file, instead of writing the actual color code again, I wrote `var(--accent)` — I
did this in 7 different places, like the button and links. The reason this matters: if I ever
want to change my site's whole color scheme, I only have to edit one line, instead of hunting
down every place the color is used.

**Where it actually shows up** (for anyone checking this is real, not generic):
[index.html, lines 29, 58, 73, 92, 118, 134, 136](index.html) all read `var(--accent)`, all
pointing back at the single `--accent: #1A52B0;` declaration defined in `:root` near the top of
the same file.
