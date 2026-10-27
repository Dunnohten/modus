# Phase 0 report: baseline and decisions

Closed 2026-10-27.

## What was done

- Published this repo (public, MIT) with the roadmap, decisions, build log and known issues.
- Ran EDH's test suite on the owner's Mac at commit 76360d4: 760 tests OK with 173 skipped (Linux-only), so 587 ran.
- Compared EDH's branches and tested the second line of work, origin/blocked-capability: 971 tests, 135 failures.
- Checked the code that stops an agent from making the owner's decisions (`_human_only`).
- Recorded the decisions: build order, license, D-E, and D-A to D-D.
- Built an import-boundary check in EDH (8 parts, 29 reasoned exceptions, 17 new tests).
- Set the license to MIT with copyright holder Tyler Dunn in all three repos: this one, EDH and Bunker Protocol (8f4898c).

## Issues faced and how they were corrected

- The first baseline (731 tests, 1 failure) was taken from an older copy of EDH. It was replaced by the Mac run above.
- The one failure seen on Linux does not appear on the Mac, so it was environment-specific.
- A plan to remove Claude's co-author trailers from this repo's history needed a force-push. Hard stop 2 blocked it, as designed. A plain push of clean commits went through instead. Four early public commits still carry the trailers. This is open.
- A rebase plan did nothing until `git fetch` restored the real remote position, because the history rewrite had moved the local tracking ref.
- An earlier note said Bunker had no license. It already had an MIT one; only the holder name changed.
- Two claims turned out wrong or unconfirmed and were corrected or marked: the reported 839 passing tests (matches neither branch tested) and the D-D claim about the agent-shell guard (it exists but has a gap).

## What it means for building Modus

- EDH has two diverged lines of work from a stale main: macOS identity (10 commits ahead) and blocked-capability (11 ahead). The baseline is the macOS line at 76360d4. Merging the two is the first job of Phase 1, after the gh test failures are explained.
- Import boundaries are now enforced in EDH. The approval layer can be built without tangling the kernel further, and the memory part imports only the base layer, which keeps it extractable later.
- The guard that refuses owner decisions from inside an agent shell exists but has a known gap (the workflows retire command). Phase 1 must build and test the refusal for loosening a stop, not assume it.

## Verified

- 760 tests OK with 173 skipped (Linux-only), so 587 ran, on the owner's Mac at 76360d4 (owner's terminal output).
- The import-boundary test fails when a new bad import is added and passes when it is removed (three temporary edits, each reverted). The full suite ran 777 tests OK with 173 skipped.
- All three LICENSE files are MIT with holder Tyler Dunn. Bunker's change is commit 8f4898c, one line (owner's terminal output). This repo's LICENSE was compared with the SPDX MIT template.
- Decisions are recorded in DECISIONS.md with their dates.

## Not verified

- The reported 839 passing tests. It matches neither branch tested.
- The cause of the 135 blocked-capability failures: code or environment is unknown.
- The 173 skipped tests on macOS, and a real agent shell being refused end to end on macOS.
- The reasons written beside the 29 import exceptions. They are the builder's reading of the code.
- The import-boundary commit (edda771) is on a local EDH branch and not published, so readers cannot open it yet.

## Gate result

Pass. All five Phase 0 boxes are ticked in ROADMAP.md: baseline recorded, license in every repo, import-boundary test passes, decisions blocking Phase 1 answered, and this report.

## Decisions made or still open

- Made: build order, license (MIT), D-E (no extraction yet), D-A to D-D.
- Open: D-F (Phase 2), D-M2 (Phase 4), the four early commits with trailers, which line is the base to merge into, and whether to fix the one non-hermetic test before Phase 1.

## Update, 2026-10-27

The report above is left as closed. These facts correct parts of it.

- `blocked-capability`, named in this report (once as `origin/blocked-capability`), is an unpublished branch from the owner's helper computer. It is not on GitHub. The Mac checkout's `origin` was a bundle file, so the `origin/` names came from that snapshot.
- GitHub has four branches: `main` (c509833, Oct 24); `armory/macos-process-identity` (76360d4, 10 ahead of main); `armory/macos-approval-mode` (8989100, 30 ahead of main, containing 76360d4); and `harness2-integration` (old).
- The reported 839 passing tests is explained. It is from `armory/macos-approval-mode`: 839 tests, OK, 244 skipped, so 595 ran. It did not match the other runs because it is a different branch.
- Not verified: the branch list and counts were seen by the helper in a fresh clone, not by us. That the 839 run was on the owner's Mac is inferred.
- The cause of the `blocked-capability` failures is now traced, so "code or environment is unknown" above no longer holds for most of them. On macOS `/var` is a symlink, so a test's temp workspace looked outside the workspace and read-only commands asked. 125 of the 135 pass with a short symlink-free `TMPDIR`. The fix, e9b8ae9, is on `armory/macos-process-identity` and absent from `blocked-capability`.
- Ten failures remain: 2 real-kill tests (macOS has no subreaper; the code refuses on purpose), 2 in `test_unreadable_shell`, 2 in `test_subscription_providers` (real Gemini CLI), 1 curl test (curl 8.7.1 help format; the test's parser is too narrow, the code looks right) and 3 untraced (`test_birth`, `test_boot`, `test_tui`), all passing at 76360d4.
- A real merge of e9b8ae9 into `blocked-capability` conflicts in 8 files and is not resolved. This bears on the Phase 1 job of merging the two lines.
- These facts were seen by the EDH session on the owner's Mac (Python 3.15.0), not by us.
