# Known issues

What is wrong or unconfirmed right now, with what is known and what is not. Dated 2026-10-27. Entries leave this list when they are fixed or confirmed, with the evidence linked in [BUILD-LOG.md](BUILD-LOG.md).

## 1. 135 test failures on `origin/blocked-capability`

**Known**
- The branch ran 971 tests with 135 failures.
- 81 are in `test_gh_delete`. It fails the same way at every commit that has it, since its first commit, 5238784.
- 26 are in `test_host_automation` and 13 are in `test_gh_destructive`. That makes 120 in the gh and host-automation modules.
- 13 more also fail on `origin/main`: `test_birth` 3, `test_durability` 2, `test_subscription_providers` 2, and one each in `test_tui`, `test_skills`, `test_safety`, `test_permissions`, `test_foundry` and `test_boot`.
- 2 are in `test_unreadable_shell`. They expect `/proc` wording that macOS does not produce.
- 120 + 13 + 2 = 135.
- `test_workers_branching` fails on main only, so it is not in the 135.
- This breakdown is taken from the owner's Mac run report. We have not seen the run ourselves.

**Not known**
- Whether the gh failures come from the code or the environment.
- Whether the 2 `test_unreadable_shell` failures are the only environment-specific ones beyond the gh modules.

## 2. A test that is not hermetic

**Known**
- One test reaches the installed Gemini CLI.

**Not known**
- Which test it is. The name is not recorded here.
- Whether its result changes on a machine without that CLI.

## 3. The reported 839 passing tests

**Known**
- A report of 839 passing tests on EDH's newest branch exists.
- It matches neither run we have: 760 on the macOS identity branch, and 971 run with 135 failures on `blocked-capability`.

**Not known**
- Where the figure came from, or which branch and commit it describes.

## 4. `workflows retire` has no human-only guard

**Known**
- The `_human_only` guard (`cli.py:834`) covers approvals, skills, plugins, foundry, workers, identity, config and postures.
- `workflows retire` is not covered.
- Many refusals have no test that was found.

**Not known**
- Whether the omission is intended.
- Whether any other command lacks a guard.
- Whether the refusal works end to end on macOS.

## 5. Four early public commits carry Claude trailers

**Known**
- `ecd62e8`, `92f401e`, `706cba5` and `debafa0` carry `Co-Authored-By` and `Claude-Session` lines.
- A local rewrite removed them. It changed no file contents, authors or dates, which was checked.
- The force-push needed to publish the rewrite was blocked by hard stop 2. A plain push of clean commits went through instead.
- Every commit after those four is clean.
- A decision on the force-push is pending.

**Not known**
- How GitHub lists contributors for the four commits.
- How long the old commits stay reachable on GitHub if the history is rewritten.
