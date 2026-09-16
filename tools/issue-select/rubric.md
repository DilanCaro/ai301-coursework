# Rubric: is this a good first issue?


<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->
## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Repository active | Inspect `archived`, `last push to any branch`, `latest release`, and `last 5 default-branch commits` in the repo-facts block. Distinguish meaningful human development from automated updates and superficial README-only maintenance. | Pass if the repository is not archived and shows meaningful human development within 120 days of the capture date. Meaningful activity includes a human-authored code or documentation commit, a release, or a bot merging a human-authored pull request. Automated dependency updates, leaderboard updates, formatting changes, or isolated superficial README edits do not establish activity by themselves. Fail if archived or if no meaningful human development occurred within 120 days. | required |
| Maintainer reachable | Inspect the maintainer first-response sample, the issue opener's association, and maintainer participation in the comment thread. | Pass if at least one sampled issue received a maintainer response within 30 days, or this issue was opened or clarified by an OWNER, MEMBER, or COLLABORATOR. Otherwise mark unclear. This is a ranking signal only and must never cause rejection. | preferred |
| Scope suitable | Read the issue body and entire available comment thread. Inspect the requested outcome, current behavior, acceptance criteria, maintainer diagnosis, unresolved design questions, tracking lists, previous claims, and linked closed pull requests. | Pass if the issue requests one coherent and observable outcome: one bug fix, feature, documentation goal, or similarly bounded contribution. A brief issue passes when it describes observable incorrect behavior or was filed or diagnosed by a maintainer. Multiple possible causes, implementation suggestions, affected files, or subtasks serving the same outcome do not make the scope unsuitable. Fail if it is a support question; a megaissue, umbrella, or tracking list; a broad codebase-wide cleanup; an unscoped feature wish requiring an unresolved product decision; or a thread with continuing disagreement about the desired behavior. Also fail when an issue older than one year has at least two closed or abandoned implementation pull requests, or at least two documented claim-and-abandon cycles, because this is evidence that the apparent task is not newcomer-sized. | required |
| Issue available | Inspect assignees, formally linked pull requests, pull requests mentioned in comments, claim comments, and later replies or automated unassignment messages. | Fail if the issue has a current assignee, an open implementing pull request, a pull request mentioned in comments that is not explicitly identified as closed or merged, or an active claim made within 90 days of the capture date. Pass when none of those conditions exists. A claim older than 90 days is stale and does not block the issue when there is no current assignee or open pull request. A closed or merged pull request does not count as an active claim. An automated unassignment message explicitly clears the corresponding claim. | required |
| Contribution permitted | Inspect the contribution-policy line, including CONTRIBUTING.md, dedicated AI-policy files, AGENTS.md, and stated contribution-tool restrictions. | Pass when the policy is silent about AI, explicitly permits AI assistance, or permits it under conditions such as disclosure, testing, review, understanding, and contributor responsibility. Fail when the policy prohibits AI-generated or AI-assisted code or documentation in a way incompatible with this course workflow. | required |

## Verdict rule

Grade each named check as pass, fail, or unclear.

Accept if and only if every required check passes.

Reject if any required check fails or is unclear. A rejection must name
every required check that failed or was unclear using its exact check name.

The preferred `Maintainer reachable` check never changes an accept verdict
to reject. A preferred failure or unclear result may only rank otherwise
accepted issues.

Do not reject an issue merely because it lacks a good-first-issue label,
has no published release, has no comments, has an old opening date, has a
short description, lists multiple possible causes, or suggests multiple
ways to achieve one outcome. Apply only the explicit conditions above.

