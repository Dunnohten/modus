# Modus

An agent you don't have to babysit. It runs on its own, stops only at a few hard lines that never move, and leaves receipts you can read afterward.

**Status: planning.** Nothing in Modus has been proven yet. This repo is where the build happens in public: the plan, the gates each step must pass, the decisions still open, and a log of what was done and what went wrong.

## What Modus is

Modus is four pieces working as one agent. Each piece is meant to be usable on its own.

| Piece | What it does | Status |
| --- | --- | --- |
| Enclave SDK | The kernel: events, permissions, workers, knowledge, evaluations | Built, but still lives inside EDH |
| Everyday Harness (EDH) | The product you sit in front of: a terminal UI with identity and personal defaults | Built; being fixed, not rebuilt |
| Bunker Protocol | The doctrine: hard stops, directives, and work marked done only with proof | Written, in its own repo |
| Memory system | Memory kept as plain markdown you own, with a rebuildable index | Designed; no code yet |

## What we are aiming for

1. A few hard stops that no setting can lift. Each needs a typed yes from a person.
2. Everything else runs unattended and leaves a receipt: what was done, what was refused, and why.
3. One yes covers a whole plan, tied to the plan's exact contents.
4. Any model works: Claude, Codex, Gemini or a local one.
5. Self-improvement only behind tests the agent cannot edit.

## Labels used here

- **Designed:** written down, no code.
- **Built:** code exists and its tests pass.
- **Proven:** a gate in the roadmap passed and the evidence is published.

Nothing is called proven before its gate passes.

## Follow along

- [ROADMAP.md](ROADMAP.md): six phases, each ending in a pass/fail gate, with checkboxes.
- [DECISIONS.md](DECISIONS.md): what is still undecided and who decides.
- [BUILD-LOG.md](BUILD-LOG.md): what was done, what went wrong, what was verified and what was not.
- [reports/](reports/): a milestone report at the close of each phase.

## License

MIT. See [LICENSE](LICENSE).
