# Open decisions

The recommendation column is a proposal, not a decision. Decisions are recorded here with the date when made.

| Decision | Question | Recommendation | Blocks |
| --- | --- | --- | --- |
| Build order | Approval layer, then scheduler plus one chat channel, then container backend, then Memory? | Yes | All phases |
| License | Which license for the front repo and the other pieces? EDH is already MIT | MIT, for consistency | Phase 0 |
| D-E | Extract Enclave as its own package now? | No; define the interface inside EDH and extract when a second user exists | Phase 0 |
| D-A | Is a push to your own feature branch "publishing"? | No for a private branch; yes for a PR on a shared repo, a tag or a release | Phase 1 |
| D-B | Where does the official wording of the stops live? | Generate the config from the pinned text in Bunker Protocol | Phase 1 |
| D-C | One typed yes per stop, or one over a listed batch? | Per stop; "yes all N" only with all N on screen | Phase 1 |
| D-D | May a stop be loosened in config? | Yes, only on a terminal with a typed phrase, logged | Phase 1 |
| D-F | Revise Bunker Protocol: real dispatch adapters and a signed approval channel? | Yes, each after an explicit yes | Phase 2 |
| D-M2 | Fix forgetting versus the tamper-evident log by chaining a salted hash and storing content separately? | Yes, for new events only | Phase 4 |

## Decided

None yet.
