# Known issues

What is wrong or unconfirmed right now, with what is known and what is not. Dated 2026-10-27. Entries leave this list when they are fixed or confirmed, with the evidence linked in [BUILD-LOG.md](BUILD-LOG.md).

## 1. 135 test failures on `blocked-capability`

**Known**
- `blocked-capability` is an unpublished branch from the owner's helper computer. It is not on GitHub.
- The branch ran 971 tests with 135 failures.
- 81 are in `test_gh_delete`. It fails the same way at every commit that has it, since its first commit, 5238784.
- 26 are in `test_host_automation` and 13 are in `test_gh_destructive`. That makes 120 in the gh and host-automation modules.
- 13 more also fail on `origin/main`: `test_birth` 3, `test_durability` 2, `test_subscription_providers` 2, and one each in `test_tui`, `test_skills`, `test_safety`, `test_permissions`, `test_foundry` and `test_boot`.
- 2 are in `test_unreadable_shell`. They expect `/proc` wording that macOS does not produce.
- 120 + 13 + 2 = 135.
- `test_workers_branching` fails on main only, so it is not in the 135.
- This breakdown is taken from the owner's Mac run report. We have not seen the run ourselves.

**Cause (seen by the EDH session on the owner's Mac, Python 3.15.0; not seen by us)**
- On macOS `/var` is a symlink, so a test's temporary workspace looked like it was outside the workspace, and read-only commands asked for approval.
- 125 of the 135 pass with a short, symlink-free `TMPDIR`. An earlier count of 127 was wrong; 125 is right.
- The fix is commit e9b8ae9, on `armory/macos-process-identity`. It is absent from `blocked-capability`.
- Ten remain:
  - 2 real-kill tests. macOS has no subreaper, and the code refuses on purpose.
  - 2 in `test_unreadable_shell`. They expect `/proc` wording that macOS does not produce.
  - 2 in `test_subscription_providers`. They reach the real Gemini CLI.
  - 1 curl test. Curl 8.7.1 formats its help differently, and the test's parser is too narrow. The code looks right.
  - 3 untraced: the `test_birth` cycle-budget probe, the `test_boot` GPU list (it shows an extra "Apple Silicon" entry), and a `test_tui` search marker. All three pass at 76360d4.

**Not known**
- Why the 3 untraced failures fail on `blocked-capability` but pass at 76360d4.
- Whether the curl test's parser or the code is at fault. The code only looks right.
- Whether the two lists of 10 and 135 line up test for test. The module counts above predate the cause trace and are not re-mapped.

## 2. A test that is not hermetic

**Known**
- One test reaches the installed Gemini CLI.

**Not known**
- Which test it is. The name is not recorded here.
- Whether its result changes on a machine without that CLI.

## 3. The reported 839 passing tests (explained)

**Known**
- The figure comes from `armory/macos-approval-mode` on GitHub (8989100, 30 commits ahead of main, and it contains 76360d4).
- That run was 839 tests, OK, 244 skipped, so 595 ran.
- It did not match the 760 on `armory/macos-process-identity` or the 971 on `blocked-capability` because it is a different branch.
- The branch list and counts were seen by the helper in a fresh clone, not by us.

**Not known**
- Whether the run was on the owner's Mac. That is inferred.
- Why 244 tests were skipped here against 173 at 76360d4. It is not recorded.

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
