# Capstone Agent Spec — Daily Search-AI Beat

## 1. Job to be done

A daily check-in agent that scans for genuinely new SEO / search-AI industry developments since
its last run and reports **only what's actually new** — no padded "brief" on a quiet day, and no
silent skipping on a day something real happened. This is FL-04's Weekly Search-AI Brief
upgraded from a fixed workflow into a real agent: instead of me handing it a topic and it running
one fixed search, **it decides how many searches to run, when it has enough sources, and whether
today's findings are worth reporting at all.**

## 2. User and usage frequency

Just me. **Daily** — a 1-2 minute check most mornings, not a scheduled/unattended job yet (see
Platform choice below for why daily-manual, not daily-automatic, is the honest scope for ~10
hours).

## 3. Tools and data needed, with access plan

| Need | Tool | Access plan |
|---|---|---|
| Live web search | Claude Project's built-in web search | Already available free on claude.ai — no setup beyond confirming it's toggled on for the Project |
| Memory of "what did I already cover" | A single **state block** (plain text: last run date + 3-5 headline facts already reported) that the agent outputs at the end of each run and I paste back in at the start of the next | No new tool — this is the realistic, zero-infrastructure way to give a Claude Project session-to-session memory. Named explicitly as a manual step, not hidden (see Risks) |
| Somewhere to keep the config | Claude Project custom instructions | Already used for FL-04; this spec's Section 4 replaces that file's Step 1 |

No other external tool, database, or write-access system is needed for the ~10-hour scope. No
account beyond the free claude.ai account I already use.

## 4. Draft instructions (delta from FL-04's fixed pipeline)

```
You maintain a daily search-AI industry beat. At the start of every run, the user pastes your
last STATE BLOCK (or says "first run" if none exists). If no state block is provided and this
isn't declared a first run, STOP and ask for it rather than assuming nothing has been covered.

LOOP (this is the agent part — you decide when to stop, not a fixed step count):
1. Run a web search on the core beat (SEO / search ranking / AI search industry news).
2. Judge the results: at least 3 credible, genuinely NEW items not already in the state block?
   If yes, move to step 3. If no, refine the query (narrower topic, different angle, or a
   named sub-topic from the state block's "watch next" list) and search again. Stop looping
   after 3 total search attempts even if still thin -- report what you have, honestly labeled.
3. For each new item: is it something the old FL-04 pipeline's Step 4 rules would flag (single
   source, stale, forbidden language)? Apply those same checks.
4. If ZERO genuinely new, verified items exist: say so in one line ("Nothing new since
   [last date] worth reporting") and STOP. Do not pad with old news restated.
5. Otherwise, draft a short brief (same format as FL-04: why it matters, 3-5 sourced bullets,
   watch next, sources) covering ONLY the new items.
6. End every run with an updated STATE BLOCK: today's date + the headline facts just reported
   (for me to paste back in tomorrow).
```

## 5. Five eval cases (defined before building)

1. **Real news day** — a genuine, verifiable industry event exists. Agent produces a properly
   sourced brief and an updated state block.
2. **Quiet day** — nothing has changed since yesterday's state block. Agent correctly outputs the
   one-line "nothing new" response and does *not* generate a padded brief. This is the core
   agent-vs-workflow test: a fixed pipeline would always produce a 5-bullet brief; an agent should
   recognize "no work needed" as a valid outcome.
3. **Thin first search** — the first search returns under 3 usable new sources. Agent
   autonomously runs a second, refined search rather than stopping cold or padding with a
   marginal source. This is the actual "loop" the FL-05 explainer identified as the missing
   agent behavior.
4. **Single-source, surprising claim** — a new item is real but only one source reports it.
   Agent must hedge it explicitly ("one source reports...") rather than presenting it as
   confirmed, same rule as FL-04's review step.
5. **Missing state block** — I forget to paste yesterday's state block and don't say "first
   run." Agent must stop and ask, not silently assume today is day one (which would either
   re-report old news as new, or worse, silently lose the memory trail).

## 6. Risks and guardrails

- **Must never fabricate a source.** If search returns nothing usable after 3 attempts, say so —
  never invent a plausible-sounding URL or claim.
- **Must never report a claim as "confirmed" on a single source.** Carried from FL-04; matters
  more here because a wrong "fact" that enters the daily state block would silently propagate
  into every future day's memory if not caught at the point it's first reported.
- **Must always show its source list before the final brief**, same as FL-04 — keeps every run
  auditable, not just the output trusted blindly.
- **Must confirm with me before ever taking an action with a real-world side effect** (posting
  anywhere, sending anything, editing a live file). Out of scope for this spec entirely — this
  agent only reads and reports — but stated explicitly so a future extension doesn't quietly
  cross that line without a new guardrail being written first.
- **Must stop and ask, never guess, when the state block is missing or ambiguous** (Eval case 5)
  — silently guessing here corrupts memory going forward, which is worse than a wrong one-off
  answer.

## 7. Platform choice, justified against an alternative

**Chosen: Claude Project with custom instructions + built-in web search.** Free, matches my
actual skill level (comfortable with code, new to running unattended infrastructure — see
`stack-decision.md`), and it's the same platform FL-04 already proved works for this exact
domain. The manual state-block hand-off is a real limitation, but it keeps the whole build inside
one free tool I already know how to run, achievable well inside 10 hours.

**Alternative considered: an n8n workflow on a daily cron trigger**, so it runs automatically
without me opening a chat. Rejected for this build, not forever: it would remove the one honest
weak point (me remembering to paste the state block) but adds real new maintenance —
self-hosting or a cloud account, a workflow file to debug when it silently breaks, and a
genuinely new tool to learn under time pressure. The FL-04 "three roads" reasoning applies again
here: pick the option that matches today's actual need (daily but manually triggered is fine)
over the more powerful option that solves a problem I don't have yet. If missing a day ever
becomes a real cost, n8n is the documented next step, not a mystery option.
