# Build log — Daily Search-AI Beat agent

Real iteration, in the order it happened. Nothing here is a retroactive clean story — the
attribution problem in Entry 1 was found by accident while trying to write Day 1's brief, not
planned in advance.

## Entry 1 — v1 instructions had a real attribution gap (found on Day 1's first search)

The spec (`capstone-agent-spec.md`) and v1 instructions said to hedge single-source claims, but
didn't say *how* to know which source a claim came from. Day 1's first search returned a bundled
summary claiming "Google launched an Intelligent Search box powered by Gemini 3.5 Flash." I tried
to verify it against the article that looked like the likely source and found that article was
explicitly a **predictions** piece from January 2026 — it didn't say what the search summary
implied it said, and I couldn't confirm any source actually made that specific claim.

**Change made:** v2 adds an explicit step — tag every fact to its source *before* judging
whether there's enough to draft, and drop anything that can't be tagged rather than trusting the
search tool's own bundled summary. This is a direct re-import of a step FL-04's pipeline already
had (Step 2 — Synthesize) that got compressed out when I first wrote this spec's shorter 6-step
loop. Cutting it turned out to be a real mistake, not just a stylistic simplification — worth
naming honestly rather than pretending v1 was fine.

## Entry 2 — the loop's step-2 refinement worked, unplanned

Because Entry 1's claim got dropped, the loop had to run a second, more specific search to reach
3 usable items. That's not a scripted demo of the "refine and re-search" behavior from the spec
— it's the first real case where dropping something forced the loop to actually do it. The
second, narrower query produced far better-sourced results (cross-tracker AI Overview stats)
than the first broad one. Real evidence the design works, found by not getting the first search
right rather than by staging a failure on purpose.

## Entry 3 — testing "quiet day" found a harder, more honest version of it

I expected Day 2 (using Day 1's real state block) to come back quiet, since it was the very next
run. It didn't — Google's actual expansion plans for the information-agents feature were real,
undisclosed-to-Day-1 news. Reported that honestly rather than forcing a quiet result to match
what I'd planned to test.

Ran a **third** pass immediately after (Day 2b), re-querying the now-resolved topic, and *that*
one came back genuinely closer to quiet — one incremental detail (a rough timeline: "summer
2026") on an already-known fact, not 3+ new items. This turned out to be a better test than a
clean synthetic "zero results" case: it checks whether the loop can tell *new information* apart
from *the same story with one more detail*, which is the actually-hard version of the judgment
call, not the easy one.

## Deviations from the FL-06 spec, and why

- **Platform for this build/test phase: Claude Code (via its web search tool), not yet a live
  claude.ai Project.** The spec named Claude Project as the target platform, and that's still the
  right call for daily personal use (reasoning unchanged from the spec). But I can't create a
  Project on the user's claude.ai account or record a screen capture of it from here — that's
  account-bound. Building and stress-testing the exact instructions against a real, live search
  tool in an environment I *can* operate and document was the honest way to do real iteration
  before asking for the one step only the account owner can do. The instructions in
  `instructions-v2.md` are unchanged by *where* they were tested and are what actually gets
  pasted into the real Project.
- **State-block hand-off tested manually, as spec'd** — no deviation here, but worth confirming
  it held up in practice: carrying the state block forward across three real runs worked exactly
  as designed, including correctly carrying forward an unresolved item (the unverified
  "Intelligent Search box" claim) across all three runs without it being dropped or silently
  turned into a fact.
- **No "3 search attempts, then report thin" case actually triggered** — every real search in
  this test run returned enough usable material within 1-2 attempts. This path is specified and
  present in v2's instructions but hasn't been exercised by a real run yet; flagging it honestly
  as untested rather than claiming full coverage.

## What's left — the one step only the account owner can do

Everything above validates the logic. What's still needed for the actual FL-07 deliverable:
1. Paste `instructions-v2.md` into a real Claude Project on claude.ai (Project → Custom
   Instructions), with web search confirmed on.
2. Run it once for real, live, unedited — first message: "first run."
3. Record that run as a raw ~2-minute screen capture, start to finish, showing the tool-use
   happening (the search running), not just the final text.
