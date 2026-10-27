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

## Corrections

- Mercury's "no approval prompts" applies to its background Bots only, not the whole agent.
- Hermes Agent has six built-in terminal backends, not seven.
- Octopus OS is closer to Modus than first stated: it already has a policy layer, an OS sandbox and a verifier-gated ledger.
- A claim about Mercury's pinned plugin checksums could not be confirmed in its source and was dropped.
