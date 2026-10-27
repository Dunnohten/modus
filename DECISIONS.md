# Open decisions

The recommendation column is a proposal, not a decision. Decisions are recorded here with the date when made.

| Decision | Question | Recommendation | Blocks |
| --- | --- | --- | --- |
| D-F | Revise Bunker Protocol: real dispatch adapters and a signed approval channel? | Yes, each after an explicit yes | Phase 2 |
| D-M2 | Fix forgetting versus the tamper-evident log by chaining a salted hash and storing content separately? | Yes, for new events only | Phase 4 |

## Phase 1 decisions in plain words

All four were decided on 2026-10-27, as recommended. The options and costs are kept here as the record of what was weighed.

### D-A: Is a push to your own feature branch "publishing"?

In plain words: does the agent need a typed yes before it pushes work to a branch only you use?

- **Option 1: every push is publishing.** Costs constant approvals on routine work, and people start approving by reflex.
- **Option 2: a push to a private feature branch is not publishing; a PR on a shared repo, a tag or a release is.** Risks "private" being assumed instead of checked. A branch on a public repo is visible to everyone, and a push can trigger CI or a deploy.
- **Recommendation: No for a private branch; yes for a PR on a shared repo, a tag or a release.**

### D-B: Where does the official wording of the stops live?

In plain words: which file is the one true text of the hard stops?

- **Option 1: generate the config from the pinned text in Bunker Protocol.** One source. Costs a dependency on the pinning step, and a change to the stops must be a deliberate update.
- **Option 2: write the stops directly in the Modus repo.** Self-contained. Risks two copies that drift apart.
- **Option 3: each harness keeps its own wording.** Most flexible. Risks drift and weaker stops, and no single text to audit.
- **Recommendation: Generate the config from the pinned text in Bunker Protocol.**

### D-C: One typed yes per stop, or one over a listed batch?

In plain words: when several stops come up together, does each get its own yes?

- **Option 1: one typed yes per stop, always.** Safest. Costs the most friction.
- **Option 2: one yes per stop, plus "yes all N" only when all N are on screen.** Less friction. Risks skimming a long list and approving without reading.
- **Recommendation: Per stop; "yes all N" only with all N on screen.**

### D-D: May a stop be loosened in config?

In plain words: can a person relax one of the hard stops, and how?

- **Option 1: never.** Stops are fixed in code. Costs a code change and a release when a stop is wrong for a real case, and people may work around it.
- **Option 2: yes, only on a terminal with a typed phrase, and logged.** Risks an agent typing the phrase itself if it shares that terminal. The log detects a loosening afterwards but does not prevent it. EDH already refuses its existing user decisions when they are requested from inside an agent shell. Extending that refusal to loosening a stop is Phase 1 work and is not yet built or tested.
- **Option 3: yes, by editing the config file.** Easiest. Risks the agent editing its own limits, which defeats protected, human-edit-only config.
- **Recommendation: Yes, only on a terminal with a typed phrase, logged.**

## Decided

- **D-A: decided 2026-10-27** (the General), as recommended. A push to a private feature branch is not publishing. A PR on a shared repo, a tag or a release is.
- **D-B: decided 2026-10-27** (the General), as recommended. Generate the config from the pinned text in Bunker Protocol.
- **D-C: decided 2026-10-27** (the General), as recommended. One typed yes per stop. "Yes all N" only with all N on screen.
- **D-D: decided 2026-10-27** (the General), as recommended. A stop may be loosened only on a terminal with a typed phrase, and the change is logged.
- **Build order, decided 2026-10-27** (the General): approval layer, then scheduler plus one chat channel, then container backend, then memory.
- **D-E: no, decided 2026-10-27** (the General). Define the Enclave interface inside EDH, and extract Enclave as its own package when a second user exists.
- **License: MIT, decided 2026-10-27** (the General). Applies to the front repo; EDH is already MIT.
