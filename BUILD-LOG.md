# Build log

What was done, what went wrong, and what was verified. Newest entries go at the bottom. "Not verified" is stated every time, because a log that only lists wins is not worth reading.

## 2026-10-27: planning day

| # | What was done | What came out | Verified? |
| --- | --- | --- | --- |
| 1 | Reviewed the Enclave SDK and Everyday Harness (EDH) specs and planned how Bunker Protocol fits in | An integration plan with hard stops, authority and origin stamping | Design only; nothing built |
| 2 | Audited the EDH repository against the plan | EDH is well ahead of expectations, so it is fixed, not rebuilt | Headers, config and targeted searches, not every module |
| 3 | Ran EDH's test suite on a copy of the repo | 731 tests ran, 1 failed, and it failed when run alone | One run, no baseline from the owner's machine. Now stale; see entry 8 |
| 4 | Designed how to cut approval friction without weakening the hard stops | A three-file config shape (stops, guards, authority) and an approval flow | Design only |
| 5 | Compared a memory-system blueprint to EDH's knowledge engine | Most of it already exists; four conflicts named | Code read, not run |
| 6 | Checked six other agent systems (Hermes Agent, OpenClaw, Mercury, DeepSeek Harness, Octopus OS, Sentient OS) against their source code, or the installed app for two | No document in the six describes absolute typed-yes stops or one approval tied to an exact plan | Docs and code read, none run. DeepSeek's sandbox behavior and OpenClaw's marketplace figures are secondhand |
| 7 | Named the combined agent Modus and wrote the six-phase roadmap | [ROADMAP.md](ROADMAP.md) | Design only |
| 8 | Found that the owner's EDH checkout is nine commits ahead of the copy audited in entry 2, including macOS identity work | The test baseline in entry 3 is stale and must be redone in Phase 0 | Seen in the commit list; not yet re-tested |
| 9 | Re-ran the EDH suite on the owner's current checkout (commit 76360d4), on Linux with Python 3.12 | 760 tests ran, 1 failed: `test_probing_stops_when_the_cycle_budget_is_spent` in `test_birth.py`. The test's fake program reports "No manual entry", so it looks environment-specific | One run on Linux, not on the Mac. A separate report of 839 passing tests on EDH's newest branch is unconfirmed here, and the counts differ, so the branch needs to be named |
| 10 | Published the front repo at github.com/Dunnohten/modus, public, MIT | The repo is live with the plan, roadmap, decisions, build log and LICENSE | Verified: GitHub reports the repo public with `main` as the default branch, and the remote tip matches the local tip. The LICENSE text was checked against the SPDX MIT template: it matches word for word except the year and copyright holder line |
| 11 | Decided the build order (approval layer, then scheduler plus one chat channel, then container backend, then memory) and D-E (no: define the Enclave interface inside EDH, extract it when a second user exists) | Both moved from the open table to Decided in [DECISIONS.md](DECISIONS.md). No roadmap box ticked | Verified: the entries are in the file and pushed. The Phase 1 decisions (D-A to D-D) are still open |
| 12 | Added a standing rule to [CLAUDE.md](CLAUDE.md): keep the repo current, tick a box only with linked evidence, write a milestone report at each phase close, never mark Proven early, never push without asking, scan before every push, no Co-Authored-By or Claude-Session lines | The rule is written down in the repo | Verified: the file exists and is pushed. Not verified: that it is followed, since no phase has closed |
| 13 | Tried to remove the Claude co-author trailers by rewriting history with `git filter-branch`. The force-push was blocked by hard stop 2, so two clean commits (decisions and CLAUDE.md) went up as a plain push instead | The rewrite worked locally: no trailer lines left, and every commit's file tree, author and date unchanged. On GitHub, four early public commits (`ecd62e8`, `92f401e`, `706cba5`, `debafa0`) still carry the trailers. A decision on whether to force-push the rewrite is pending | Verified: the local rewrite (log, trees and old-tip diff all checked), the backup bundle, and that the plain push landed with no trailers in the two new commits. Not verified: how GitHub shows contributors for the old commits |
| 14 | Recorded a claim in [DECISIONS.md](DECISIONS.md) (D-D) that EDH already refuses its existing user decisions when they are requested from inside an agent shell | The claim is public. Its source is EDH's CLAUDE.md | Not verified: it has not been checked against EDH's code. To check in Phase 0 |

## Corrections

- Mercury's "no approval prompts" applies to its background Bots only, not the whole agent.
- Hermes Agent has six built-in terminal backends, not seven.
- Octopus OS is closer to Modus than first stated: it already has a policy layer, an OS sandbox and a verifier-gated ledger.
- A claim about Mercury's pinned plugin checksums could not be confirmed in its source and was dropped.
- The first rebase plan (entry 13) did nothing until `git fetch` restored the real `origin/main`. `git filter-branch --all` had also rewritten the local `origin/main` tracking ref, so it pointed at a rewritten commit, not at what GitHub held.
