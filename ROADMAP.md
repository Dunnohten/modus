# Roadmap

Six phases. Each ends in a pass/fail gate, and a phase counts as done only when its gate passes. There are no dates; dates are added only when the owner sets them. The order is proposed until the owner confirms it.

Every phase ends with a milestone report covering what was done, issues faced and how they were fixed, and what it means for Modus. Reports are linked here when a phase closes.

## Phase 0: baseline and decisions

Re-run the full EDH test suite on the current code for a real baseline, and explain any failure. Pick one license. Add a module manifest and a test that blocks one part importing another's internals. Answer the open decisions that block Phase 1.

- [ ] The test baseline is recorded, and any failure is explained and tracked
- [ ] A license is chosen and present in every repo
- [ ] The import-boundary test passes
- [ ] The decisions blocking Phase 1 are answered
- [ ] Milestone report published

## Phase 1: approval layer

Stops, guards and authority files load as protected, human-edit-only config. The kernel classifies every action. A plan approval is bound to the plan's exact contents and expires. Safe repeats are allowed for the session. Reading untrusted content pauses risky actions. A receipts digest summarizes each run.

- [ ] Stops, guards and authority files load as protected config
- [ ] Zero missed parks, and stops hold under any grant
- [ ] Plan approval is tied to the plan's exact contents
- [ ] A web page carrying injected instructions parks instead of acting
- [ ] Milestone report published

## Phase 2: reach

A scheduler built from standing orders. A signed trusted-origin channel. One chat channel with an allowlist of fixed IDs.

- [ ] A standing order runs unattended and ends in a receipts digest
- [ ] A message from an unlisted ID is ignored
- [ ] A channel message cannot lift a stop
- [ ] Milestone report published

## Phase 3: isolation

One execution contract: run a command in an image with the worktree mounted and the network off by default. A Docker adapter. Work that read untrusted content goes to the container.

- [ ] Tainted work runs only in the container
- [ ] The network is off by default, and that is tested
- [ ] Swapping the adapter changes no kernel code
- [ ] Milestone report published

## Phase 4: memory

The memory system, step by step: markdown as the source of truth, a rebuildable index, recall receipts.

- [ ] Each Memory Gauntlet step passes before the next begins
- [ ] Milestone report published

## Phase 5: prove and publish

An end-to-end demo, an honest README, a security policy, and a first tagged release.

- [ ] A stranger runs the demo from the README alone
- [ ] Every claim about other agents is sourced and dated
- [ ] A scan finds no secrets, personal paths or account details
- [ ] Milestone report published

## What this does not promise

No dates. No feature parity with other agents: one chat channel and no native apps. No claim that Modus is safer than anything until the Phase 1 gate passes.
