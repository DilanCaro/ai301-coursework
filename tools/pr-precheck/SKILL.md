---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: **is this
ready to submit?** A PR package is a candidate pull request (title,
description, commits, unified diff, and test evidence), read against
the plan it claims to implement and the issue that plan belongs to.
You do not answer from gut feel, and you do not invent checks: you
answer by executing the student-authored grading procedure in
`procedure.md`, which applies the rubric in `rubric.md` to evidence
gathered per `references/evidence-guide.md`.

## The question

Answer exactly one question about exactly one package: is this PR
ready to submit? Grade only the package in front of you. Never grade
more than one package per run, never answer a different question, and
never substitute polish or confidence for the rubric's pass
conditions.

## Inputs and modes

One of:

- **Live mode**: the student's own submission, checked before it goes
  out. Inputs: their `plan.md` (including any deviation notes), the
  diff on their branch relative to the repo's default branch (produce
  it with `git diff main...HEAD` from the working copy, substituting
  the default branch name if it is not `main`), their draft PR title
  and description (often in `pr_draft.md`), and their test evidence
  (often in `test_evidence.md`), read against their issue. A
  house-chain student reads the house plan and the house repro pack
  instead of a personal plan/repro; the same checks still grade the
  same families of evidence. Gather issue-side and repo-side facts
  live (thread, PR template, stated contribution or AI policy) as the
  evidence guide directs.
- **Eval mode**: a package bundle is the whole world. Every fact comes
  from the bundle text; nothing is fetched and nothing else is read.
  Eval mode always grades a complete package: every check, full
  verdict rule. Ignore `scope.md` and `voice-guide.md` entirely.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else. It names where the student's PR must live and the house rules of
that environment. Refuse to grade work outside the scoped repo. If the
scope's repo line still carries an unfilled placeholder
(`<ORG>/<PATH-REVIEW-REPO>` or similar), stop without grading and tell
the student to get their cohort's scope file from the instructor;
never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`. Hold the outgoing PR title
and description against those rules and report any broken rule in the
readable summary, quoting the rule. The voice guide never changes the
verdict on its own unless the rubric has a check that reads it. In
eval mode, ignore `voice-guide.md` entirely: voice is personal and
carries no gold labels; universal communication-quality checks live in
the rubric.

## Component reads

- `rubric.md` defines the checks and the verdict rule.
- `references/evidence-guide.md` maps where each evidence family lives
  and what good looks like.
- `procedure.md` is the operating procedure: follow it as written.

If the procedure is silent on a step, report the gap in the summary;
do not improvise around it. If `rubric.md` has no checks filled in, or
`procedure.md` has no steps filled in, refuse to grade and say so:
this skill cannot grade without a rubric AND a procedure, by design.
Instruction comments inside templates are not content.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict. Emit a fenced JSON block, then
nothing else after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

Before the JSON block you may show a short readable summary (a line
per check, plus any voice-guide notes in live mode). The JSON block is
the machine-read result: the eval harness parses the last fenced JSON
block in your output, so it must be present, valid, and last.

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready
  and a beautiful confident one can hide drift. Every check reads the
  artifact itself against the plan, the issue, and the stated
  standards, never the formatting.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it still passes. The fix belongs in the
  rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as
  written, and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. If the rule
  is silent, treat `unclear` as `fail`: a PR you cannot verify from
  the package is a PR that is not ready to submit.
