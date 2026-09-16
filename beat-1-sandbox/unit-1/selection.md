# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

**Verdict output**

## Summary

**Issue #72:** `verify_password` raises `UnknownHashError` on malformed stored hashes instead of returning `False`.

| Check                  | Grade | Evidence                                                                                                                                              |
| ---------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Repository active      | pass  | Not archived; last pushed 2026-09-10; recent default-branch commits by human author Aburke225 include meaningful documentation, CI, and test changes. |
| Maintainer reachable   | pass  | Issue opened by a collaborator (`author_association: COLLABORATOR`).                                                                                  |
| Scope suitable         | pass  | One bounded fix: fail closed instead of raising, update two named files, and remove the `xfail` marker for test H-05.                                 |
| Issue available        | pass  | No assignees, comments, linked or mentioned pull requests, or claim comments.                                                                         |
| Contribution permitted | pass  | No `CONTRIBUTING.md`, `AGENTS.md`, or AI policy files were found; the policy is silent on AI use.                                                     |

All required checks pass → **accept**.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
  "checks": [
    {
      "name": "Repository active",
      "grade": "pass",
      "evidence": "Repo not archived; pushed_at 2026-09-10T21:31:21Z and last default-branch commits by human author Aburke225 (docs/ci/test commits) on 2026-08-24, both well within 120 days of capture date 2026-09-15"
    },
    {
      "name": "Maintainer reachable",
      "grade": "pass",
      "evidence": "Issue 72's author_association is COLLABORATOR, so it was opened by a COLLABORATOR"
    },
    {
      "name": "Scope suitable",
      "grade": "pass",
      "evidence": "Body requests one bounded outcome: make verify_password fail closed (return False) instead of raising UnknownHashError on malformed hashes, names two relevant files, references a specific xfail test (H-05) to un-mark, and estimates 1-2 hours"
    },
    {
      "name": "Issue available",
      "grade": "pass",
      "evidence": "assignees: [] and 0 comments; issues/72/timeline shows only 'labeled' events, no linked or mentioned pull requests, no claim comments"
    },
    {
      "name": "Contribution permitted",
      "grade": "pass",
      "evidence": "CONTRIBUTING.md, .github/CONTRIBUTING.md, AGENTS.md, AI_POLICY.md, and AI_USAGE_POLICY.md all returned 'Not Found' via the GitHub API; policy is silent on AI use"
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

agreement: 2/3 scored items
agreement: 15/19 scored items — one additional item errored because the model did not produce a fenced JSON block.
agreement: 16/20 scored items (bar: 18/20: below the bar)
agreement: 20/20 scored items (bar: 18/20: PASS)

The final run reported:

categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)

**Issue analysis**


I analyzed `issue-07`. My rubric’s final decision was `reject`, and its gold label was also `reject`.

The issue bundle stated:

> `last push to any branch: 2025-02-27`

The most recent listed human changes were superficial README edits:

> `2025-02-10 by soerenwolfers: Update README.md`

The maintainer-response sample also showed `no maintainer comment in thread` for all five sampled issues. My earlier rubric used a 180-day activity threshold, causing this repository to pass the activity check and producing an incorrect `accept`. I changed the threshold to 120 days and clarified that isolated superficial README changes do not demonstrate meaningful development. Under the revised check, the repository failed `Repository active`, resulting in the correct `reject` verdict.
**Check rationale**


My final rubric includes the following check:

> `Repository active | Inspect archived, last push to any branch, latest release, and last 5 default-branch commits in the repo-facts block. Distinguish meaningful human development from automated updates and superficial README-only maintenance. | Pass if the repository is not archived and shows meaningful human development within 120 days of the capture date. Meaningful activity includes a human-authored code or documentation commit, a release, or a bot merging a human-authored pull request. Automated dependency updates, leaderboard updates, formatting changes, or isolated superficial README edits do not establish activity by themselves. Fail if archived or if no meaningful human development occurred within 120 days. | required`

I made this check required because a clearly described issue is still a poor first-contribution target when the repository is unlikely to review or merge new work. The 120-day threshold distinguishes temporarily quiet projects from repositories showing stronger signs of abandonment. Defining meaningful development also prevents automated updates or isolated superficial changes from making an inactive project appear healthy.

**Trade-offs**

This check may reject a legitimate issue in a mature or stable project that intentionally changes infrequently. Such a repository could remain useful and still accept occasional contributions despite going more than 120 days without meaningful development.

I accepted this trade-off because this rubric is intended to identify dependable first-contribution opportunities. For a first contributor, receiving timely review and feedback is particularly important. In `issue-07`, tightening the activity check changed the result from an incorrect `accept` to the gold-label `reject`.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to my interests and available time**

   Issue #72 is a strong fit for my Python and security background. It involves changing `verify_password` so that an unknown password-hash algorithm fails closed instead of raising `UnknownHashError`. This is security-adjacent behavior with a clear expected result. The issue is estimated at approximately one to two hours and identifies an existing test that can be removed from `xfail`, so its scope is appropriate for the available course time.

2. **What the verdict identified correctly, and what I considered separately**

   The verdict correctly identified that the repository is active, the maintainer is reachable, the issue has bounded scope, nobody is currently assigned or working on it, and the repository has no contribution policy that prohibits the course’s AI-assisted workflow.

   The rubric did not directly measure how closely the issue matched my existing experience or how efficiently I could complete it. I separately considered my familiarity with Python, testing, authentication behavior, and secure failure handling. I also preferred this issue because it names the relevant behavior and provides an existing test to update, reducing the amount of exploratory work required.

3. **Anticipated difficulty in claiming the issue**

   I anticipate low difficulty claiming this issue because it currently has no assignee, comments, linked pull requests, or claim activity. It is also explicitly labeled as a good first issue. Other students may select the same issue, but the Path Review house rule allows multiple students to work on one issue because course credit is associated with the pull request rather than whether the contribution is ultimately merged.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
