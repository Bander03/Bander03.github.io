# FL-07 — Daily Search-AI Beat, Checkpoint 1 build

Spec: [`../capstone-agent-spec.md`](../capstone-agent-spec.md)

## What's in this folder

| File | What it is |
|---|---|
| [`instructions-v1.md`](instructions-v1.md) | First version of the agent instructions, as directly spec'd |
| [`run-day1.md`](run-day1.md) | Real Day-1 run against v1 — this is where the attribution gap was found |
| [`instructions-v2.md`](instructions-v2.md) | Revised instructions, fixing the gap Day 1 found |
| [`run-day2.md`](run-day2.md) | Real Day-2 run against v2, using Day 1's real state block |
| [`run-day2b-quiet-day-test.md`](run-day2b-quiet-day-test.md) | Deliberate same-day re-run testing the "nothing new" path |
| [`BUILD-LOG.md`](BUILD-LOG.md) | What broke, what changed, what's deviated from spec and why |

## Status against the FL-07 pass criteria

- **Completes the core job end to end, no mid-run hand-editing:** yes, across three real runs
  (Day 1, Day 2, Day 2b) — search → judge → tag/hedge → draft-or-decline → state block, no step
  skipped or patched by hand.
- **At least one live tool/data connection in use:** yes — every run above used real, live web
  search; nothing in `run-day1.md` / `run-day2.md` / `run-day2b...md` is fabricated or simulated.
- **Matches the FL-06 spec, or deviations documented:** one real deviation (build/test platform
  was Claude Code, not yet a live claude.ai Project) — explained in `BUILD-LOG.md`, with the
  instructions text itself unchanged by where it was tested.
- **Build log shows real iteration, not a retroactive clean story:** yes — Entry 1's attribution
  bug was found by accident mid-run, not planned; Entry 3's quiet-day test didn't go as expected
  on the first try and that's reported honestly rather than smoothed over.
- **Raw ~2-minute run capture:** **not yet done — this is the one remaining step, and it has to
  happen on your own claude.ai account.** See below.

## Your remaining step

1. Open claude.ai → Projects → new Project (e.g. "Daily Search-AI Beat").
2. Paste the contents of [`instructions-v2.md`](instructions-v2.md)'s code block into the
   Project's Custom Instructions field. Confirm web search is enabled for the Project.
3. Start screen recording, then send `first run` as your first message.
4. Let it run completely — don't edit or redirect mid-run. Once it produces a brief (or a
   "nothing new" response) and a state block, stop recording. That's your ~2-minute raw capture.
5. Submit: this folder's link, plus the screen recording file.
