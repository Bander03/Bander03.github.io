# Content Map — Bander Sidiq Portfolio

## The through-line

**One sentence:** I turn raw search and ranking data into models people can actually trust and act on.

This is the single claim every section has to earn: not "I know ML," but *I make ML explainable
enough to be usable* — visible in the baseline-vs-model comparison, the reason codes, and the
honest framing throughout the FlyRank case study.

## Site map

One page, four sections, in this order:

| # | Section | Purpose | CTA |
|---|---|---|---|
| 1 | Hero | State the through-line sentence in one glance | **Primary CTA:** "View the code" → github.com/Bander03/FlyRank_Intern |
| 2 | Case study — FlyRank Refresh Model | Prove the claim with one real project, real numbers, real charts | **Secondary CTA:** "Read the model report" → GitHub link to `outputs/model_report.md` |
| 3 | About | Who's behind the work, briefly | **Tertiary CTA:** "See all repos" → GitHub profile |
| 4 | Footer | Contact + links | Email / GitHub / LinkedIn (as available) |

Every CTA ladders to the same Week 1 action: **send visitors to view my code on GitHub.** No
competing calls-to-action (no newsletter signup, no unrelated links) — one goal per page.

## Case study content (Section 2) — what's already proven vs. what's still needed

**Proven (safe to state, backed by `outputs/model_report.md`):**
- Baseline rule Precision@50 = 0.24 → Random Forest Precision@50 = 0.74 (client-holdout split, on
  the anonymized 30k-row sample)
- Top drivers: `days_with_impressions`, `log_impressions_90d`, `avg_position` — a readable,
  inspectable model, not a black box
- Output is a ranked, reason-coded review queue, not an auto-publish decision (honest framing,
  no overclaiming — see `writing-honest-claims` skill)

**Proof still needed (not yet available, flagged rather than faked):**
- No real screenshot of a live dashboard/UI exists yet — the case study uses the SVG charts the
  pipeline itself generates (`outputs/charts/*.svg`), which *are* real, not mockups
- No client testimonial or production deployment result yet — the report explicitly says
  "reviewer aid, not automatic publishing," and the site should say the same
- No personal headshot yet — About section placeholders it; see `image-curation.md` for the
  rejection note explaining why an AI-generated headshot was not used instead

## Notes for reviewers

The site is intentionally one page. A student portfolio with five thin pages reads worse than one
page that actually proves something. Depth over surface area.
