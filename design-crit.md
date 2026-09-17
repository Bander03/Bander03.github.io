# Design Crit — Week 7 ("Survive the Crit")

**Proof statement given to the reviewer:** "I turn raw search and ranking data into models
people can actually trust and act on."

**Reviewer's brief on the two opening questions:**
1. *In 10 seconds, what do I think you do?* — "Applied ML for search/ranking... take
   search/content/ranking data → build ML models → use them to help humans decide what to
   review or improve." Specific, not "generic AI engineer."
2. *Would I believe you're good at it?* — "I'd believe you have done real ML work. I would not
   yet be fully convinced that you're very good at it." The case study (baseline, model, metric,
   holdout) is more credible than most portfolio sites, but the site stops just short of
   demonstrating judgment, not just a result.

Full raw feedback is preserved as the reviewer sent it — see the conversation this fix log came
from; not re-pasted in full here to keep this doc focused on the sort and the response.

## Sorted: must-fix vs. nice-to-have

### Must-fix (fixed on the live site today)

1. **"CV (add link)" pill** — reviewer named this "the biggest offender," explicitly unfinished
   and credibility-damaging. **Fix:** removed the dead pill entirely rather than leave a TODO
   live — LinkedIn (already present) covers the same job honestly, without a fake or broken link.
2. **The 0.24→0.74 number invites "why so dramatic?" before the honesty caveat is reached** —
   the caveat existed but was buried below the charts. **Fix:** added a one-line caveat directly
   under the stat row, linking down to the full explanation, so the context arrives before doubt
   does.
3. **"I don't see you behind the model"** — the core credibility gap: no visible method choice,
   no alternatives considered, no real difficulty named. **Fix:** added a "Behind the model"
   section with three concrete, specific things: why Logistic Regression before Random Forest,
   the actual hardest call (the Week-4 finding that position doesn't cleanly predict CTR), and
   one un-smoothed result (Logistic Regression beating Random Forest at one cutoff, reported
   rather than hidden).
4. **No clear professional ask** — reviewer suggested a direct CTA near contact. **Fix:** added
   "Open to ML/AI opportunities and research collaborations" above the contact form.
5. **"Coming as the track finishes" reads like an unfinished stub** — cheap wording fix,
   reworded to "in progress, publishing as the track wraps up."

### Nice-to-have (acknowledged, not changed today — and why)

- **Real photo instead of the placeholder.** The reviewer called the placeholder itself
  "understandable" — it's a deliberate choice from Week 3 (`image-curation.md`: a labeled
  placeholder beats a synthetic AI face). Swapping in a real photo is still the plan, just not a
  same-day fix.
- **Two more substantial case studies "demonstrating different dimensions."** This is real,
  correct advice — and it's exactly what the "Capstone & notes" section already exists to fill
  as the internship continues. Rushing a second project today to pad the site would be the
  opposite of the honesty this whole portfolio is built around.
- **Narrower vs. broader positioning.** Not a bug — a strategic question. The "search/ranking ML
  specialist" framing was a deliberate choice going back to Week 1's research question, not an
  accident. Worth revisiting consciously later, not reflexively changing because one reviewer
  flagged it.

## Response sent back to the reviewer

> Thanks — this is exactly the kind of feedback I needed. Fixed today: killed the dead "CV"
> link, moved the honesty caveat right under the headline number instead of burying it, and
> added a "Behind the model" section answering the three things you actually wanted to know —
> why Logistic Regression before Random Forest, the hardest call I made, and one result I didn't
> smooth over. Also added a direct "open to opportunities" line near contact. Holding off on a
> second case study and a real photo — those are real, correct calls, just bigger asks than a
> same-day fix, and I'd rather ship them for real later than pad the site now.
