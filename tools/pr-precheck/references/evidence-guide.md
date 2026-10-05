# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives.** In an eval bundle: the plan-context block's scope
pair (in scope / not in scope), named files or areas, approach, and
any deviation or deferral notes; then the candidate PR's unified diff,
commit list, title, and description fidelity claims. In live mode:
`plan.md` (including its deviations section), `git diff main...HEAD`
(or the default-branch three-dot diff) from the working copy, and the
draft title/description in `pr_draft.md` or equivalent.

**What good looks like.** Every material changed file and behavior
falls inside the plan's stated boundary or a recorded deviation note
that re-ties the mismatch. Planned work that is still claimed appears
in the diff, or is honestly deferred in both the plan note and the
description. Silent drift is either more than the plan (extra flags,
rewrites, unrelated files) or less than the plan still claims, with no
note. A description that claims "exactly as planned" or "no changes
beyond the plan" while the diff drifted is plan-fidelity failure, not
a polish problem.

## Test evidence (harness category: not-tested)

**Where it lives.** In an eval bundle: the plan-context test plan and
repro evidence beside the candidate PR's test-evidence section. In
live mode: the test plan in `plan.md`, the Unit 2 / house repro steps,
and the captured output in `test_evidence.md` (before/after plus the
repo's own check command outcome).

**What good looks like.** The evidence names an observable behavior,
shows the before and after (or an equivalent decisive artifact) for
the plan's named failing case through the changed path, and shows the
repo's own checks with the outcome visible—or an honest note naming a
failing check and why. "Tests pass", "works on my machine", or
evidence that only exercises an unchanged control path is not
decisive. Omitting a plan-named decisive case without an honest
deferral is not decisive.

## Diff quality (harness category: unreviewable)

**Where it lives.** In an eval bundle: the candidate PR's unified diff
and commit list. In live mode: the same three-dot branch diff and
`git log` / commit subjects on the branch.

**What good looks like.** The planned fix is visible without wading
through debris. Bad tells: debug `print`/`eprintln` leftovers,
commented-out experiments, dead helpers left behind
`allow(dead_code)`, TODO litter on imports, pure formatting or import
churn hunks, drive-by edits outside the plan, and commits titled
`wip` / `fix` / `fmt + cleanup` that bury the change. Adjacent
mechanical churn around a right fix still fails when it obscures
review.

## Standards and comms (harness category: standards-wall)

**Where it lives.** In an eval bundle: the repo-facts block's PR
template asks, contribution instructions, and stated AI-use policy,
plus any explicit maintainer template direction in the thread
highlights; then the candidate PR description's filled sections. In
live mode: `.github/PULL_REQUEST_TEMPLATE.md`, `CONTRIBUTING.md` or
equivalent policy files in the scoped repo, and the draft description.

**What good looks like.** Every required template section has real
content (closes/fixes line, checklist items, type-of-change,
changelog/whatsnew entry when asked, test notes the template
requires). When the repo states an AI-disclosure policy, the
description discloses the tool and extent of assistance in the
author's own words. Blank sections, ignored checklists, missing
whatsnew entries the template requires, or missing required AI
disclosure fail. Whether the description's change claims match the
diff is plan fidelity above, not this family.
