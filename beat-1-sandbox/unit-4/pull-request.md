# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/92

**Branch**

`fix/72-malformed-hash`

**pr-precheck verdict on draft**

**accept** (live mode on draft before opening)

Summary: all five required checks passed (plan-faithful diff, description matches diff,
decisive test evidence, reviewable diff, template and disclosure).

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
  "checks": [
    {"name": "Plan-faithful diff", "grade": "pass", "evidence": "Diff touches only core/security.py (import UnknownHashError, try/except around existing verify call, return False) and tests/unit/test_security.py (removes only the H-05 xfail marker) — exactly plan.md's named files/approach, no extra or missing deliverables."},
    {"name": "Description matches diff", "grade": "pass", "evidence": "pr_draft.md's Changes/Summary list exactly the two edits present in the diff; 'Scope matches the posted plan' is true to the diff, and unchecked Testing boxes (CI-green, integration) are left honestly unchecked, not falsely claimed."},
    {"name": "Decisive test evidence", "grade": "pass", "evidence": "test_evidence.md shows before (FAILED/UnknownHashError via --runxfail) and after (PASSED) on the plan-named case, a direct-call trigger returning False, valid-hash controls, and make lint/typecheck/test-unit outcomes; test-integration is honestly noted as not run per the plan's required-checks scope."},
    {"name": "Reviewable diff", "grade": "pass", "evidence": "git log main..HEAD is one commit, 2 files changed, 5 insertions/5 deletions, no debris, no unrelated hunks."},
    {"name": "Template and disclosure", "grade": "pass", "evidence": "All PULL_REQUEST_TEMPLATE.md sections filled with real content (Closes #72, Changes, Testing with honest unchecked items explained, N/A justified for Screenshots); repo has no stated AI policy, and the author discloses AI assistance anyway in their own words."}
  ],
  "verdict": "accept"
}
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `agreement: 20/20 scored items  (bar: 18/20: PASS)`

This was the only full scored run. The last (only) score matches the agreement line in
`eval-run.txt`.

**Package analysis**

I analyzed `pkg-20` (category: standards-wall). My rubric decided `reject`, and the gold
label was also `reject`.

Gold note: excellent bounded fix with decisive evidence, but the description contains no
AI-use disclosure and ghostty's stated policy requires disclosing all AI usage.

My Template and disclosure check requires the PR description to meet every required
template ask and any stated AI-disclosure policy. The package's repo-facts block states
that AI usage must be disclosed; the candidate description omitted that disclosure. The
code and evidence were otherwise strong, but the standards check is required, so the
verdict was `reject`. That matches the gold label and confirmed the check can see the
standards-wall category (the 2-package floor this week).

**Check rationale**

My uploaded `tools/pr-precheck/rubric.md` includes this check:

> `| Template and disclosure | Read the PR description against the repo-facts block's PR-template asks, contribution instructions, and stated AI-use policy (and any explicit maintainer template direction in the thread). In live mode, read the repo's `.github/PULL_REQUEST_TEMPLATE.md` and contribution/AI policy the same way. | Pass when every required template section the repo asks for is filled with real content (not left blank or boilerplate-ignored), and when any stated AI-disclosure requirement is met in the author's own words. If the repo states no AI policy and no applicable template ask, those absences are not failures. Fail when a required checklist item, closes/fixes line, changelog/whatsnew ask, or required AI disclosure is visibly unmet. | required |`

I wrote it this way because the lecture and eval set treat template/disclosure misses as
their own failure family, and the standards-wall category has only two scored packages —
a rubric without this surface cannot clear the category floor. I rejected a polish-only
comms check in favor of this outcome rule: fill required sections with real content, and
meet disclosure when the repo states it. That wording is what rejected `pkg-01` (pandas
checklist / whatsnew missing) and `pkg-20` (missing AI disclosure) while still accepting
terse but complete PRs such as `pkg-11` and `pkg-19`.

**Trade-offs**

The Template and disclosure check will reject an otherwise correct, well-evidenced fix
when required disclosure or checklist items are absent (`pkg-20` is the case). I accept
that miss-of-substance trade-off because the course treats standards compliance as a
submit gate, not optional polish.

Nothing else changed after the confirming full run: agreement was already `20/20` with
every category matched (`clear-accept 7/7`, `not-tested 4/4`, `silent-drift 4/4`,
`standards-wall 2/2`, `unreviewable 3/3`), so no `--only` revise loop was needed. I know
nothing flipped because there was only one scored full run and its category tallies are
complete in `eval-run.txt`.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
