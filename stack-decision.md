# Stack Decision — "Three Roads"

## 1. My four constraints

- **Budget:** free only. No paid tiers, no domain purchase required.
- **Skill level (honest):** comfortable with code — I can read and write HTML/CSS/JS/Python — but
  I'm new to actually running a deploy pipeline myself (git remotes, hosting dashboards, build
  steps). I don't want to learn a whole new toolchain in week 4 just to ship a portfolio.
- **What the portfolio needs to do:** matches the sitemap in [content-map.md](content-map.md) —
  one page, four sections in order (hero → case study → about → footer), every CTA pointing at
  my GitHub. Not a multi-page site yet.
- **How the work must be displayed:** real chart images (the SVGs my ML pipeline generates), a
  stat row of hard numbers, long-form-ish paragraph text for the case study writeup, and outbound
  links to a code repo. No image gallery of dozens of photos, no embedded interactive demo.
- **Does anything need to be dynamic yet? No.** Nothing on the site needs a database, a form
  submission, user accounts, or a live app embed. Everything is either static text, a static
  image, or a link out to somewhere else (GitHub) that already does the "live" part.

## 2. Three options, simplest to most powerful

### Option A — Plain HTML/CSS, hand-written

- **How you'd build it:** one `index.html` file, inline `<style>`, no build step, no package
  manager, no framework. Google Fonts via a `<link>` tag.
- **Where you'd host it (free):** GitHub Pages, deploying straight from the repo's `main` branch
  — no separate hosting account, no CLI beyond `git push`.
- **Backend needed?** No.
- **Real trade-off:** every layout change is manual — no shared header/footer component, no
  templating. Fine for one page; would get repetitive fast past 3–4 pages.

### Option B — Static site generator (e.g. Eleventy or Jekyll) + Netlify/Cloudflare Pages

- **How you'd build it:** write content in templated files (Markdown/Nunjucks or Liquid), the
  generator assembles shared layouts and outputs plain HTML at build time.
- **Where you'd host it (free):** Netlify, Cloudflare Pages, or Vercel — all have a free tier
  that auto-builds on every git push.
- **Backend needed?** No — still outputs static files, just with a build step in front.
- **Real trade-off:** genuinely more power once the site grows (shared nav/footer, reusable case
  study template for a second or third project) — but it's a new toolchain to learn (templating
  syntax, a `_config` file, a build command that can fail in ways plain HTML never does) for a
  site that's currently one page.

### Option C — Full framework with app capability (e.g. Next.js) or a no-code platform (e.g. Webflow)

- **How you'd build it:** either React components + routing (Next.js) or a visual drag-and-drop
  builder (Webflow) with CMS collections for content.
- **Where you'd host it (free):** Vercel free tier for Next.js; Webflow's free tier for the
  no-code route (with real limits — a `webflow.io` subdomain, no custom domain, usage caps).
- **Backend needed?** Not required today, but this is the option that makes it *easy* to add one
  later (API routes, a CMS backend) — power I'm not using yet.
- **Real trade-off:** most capable if the portfolio grows into something with forms, a blog, or
  a real CMS — but also the most to maintain: framework version bumps, a build pipeline that can
  break on dependency updates, and (for Webflow) a free-tier ceiling I'd hit before I needed the
  power in the first place.

## 3. Pressure-testing the front-runner (Option A)

- **What breaks if I pick the simplest?** Nothing breaks for what the site needs to do *now* —
  one page, static content. It would start to hurt if I added a second and third case-study page
  and had to copy-paste the header/footer/CSS into each one by hand. That's a real future cost,
  not a current one.
- **What would I maintain if I picked the most powerful (Option C)?** A framework version, a
  build pipeline, and (for Next.js) a whole app-routing structure — for a page that has zero
  interactivity today. That's maintenance load with no corresponding feature I'm using.
- **Can I finish in two weeks?** Option A: already done — it shipped the same day, and it's live
  today. Option B is realistically also a two-week job, but most of that time would go to
  learning the generator instead of writing content. Option C would eat the two weeks on
  framework setup alone, for a static portfolio that doesn't need what it buys.
- **Does it show my work the way it needs to be shown?** Yes. The case study is a stat row plus
  real chart images plus a paragraph plus outbound links — that's four `<div>`s and an `<img>`
  tag in plain HTML. No gallery plugin, no CMS collection, no framework component was ever
  required to display exactly what I have.

## 4. Decision

**Chosen: Option A — plain HTML/CSS on GitHub Pages.** It's what I already built and deployed
(`github.com/Bander03/portfolio`, live at `bander03.github.io/portfolio`), and going through
this exercise afterward didn't change my mind — if anything it confirmed it. My honest skill
level is "comfortable with code, new to deploying," and Option A asks the least of the "new to
deploying" half: one repo, one `git push`, no build step that can fail in an unfamiliar way while
I'm still learning what a normal deploy even looks like. **Can I maintain this?** Yes — it's a
single file I can read top to bottom, so if something breaks I'll know where to look, instead of
debugging a build tool I don't understand yet. **Does it show my work well?** Yes — real charts,
real numbers, real links, nothing decorative competing with them, which is the whole design
principle from Week 3.

**Why not Option B?** It's the right call the moment I have a second or third project to feature
and the copy-paste header/footer starts actually costing time. Right now that cost doesn't exist
yet — I'd be learning a templating tool to solve a problem I don't have.

**Why not Option C?** It solves for dynamic content and a CMS backend, and my own constraint
answer in step 1 was explicit: nothing needs to be dynamic yet. Picking the most powerful option
before I need its power is exactly the kind of decision this exercise is meant to catch — more
to maintain, more to break, for capability sitting unused. If the portfolio ever needs a working
contact form or a blog with dozens of posts, that's the point where I'd revisit this, not before.
