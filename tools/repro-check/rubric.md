# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment fidelity | Compare the issue's stated target and trigger conditions with the repro report's environment record: relevant tool/app version, OS or platform, runtime/browser/backend, install or build form, and configuration. Read any differences together with the report's explanation of them. | Pass when the report identifies the environment details needed to place the attempt and either tests the issue's target environment or explicitly names each material deviation and explains why the attempt still bears on the issue. Fail when a missing or silent difference could change the reported behavior, including an unreported old version, build profile, platform, backend, driver, or required configuration. | required |
| Followable reproduction | Read the repro report's starting state, commands or actions, inputs, configuration, and trigger sequence. Check them against the issue's described trigger and the repo's bug-report asks. | Pass when a stranger can recreate the relevant starting state and execute the attempt from start to trigger using the information shared in the report. Public links or pasted minimal inputs/configuration may supply details. Fail when a required command, action, option, input, configuration, or trigger is omitted or replaced; when the procedure depends on an unavailable private repository or unshared file; or when the steps exercise a materially different path. | required |
| Behavior evidence | Read the report's observable artifacts—terminal output, logs, measurements, screenshots described in text, generated output, or control results—against the issue's actual and expected behavior. For a cannot-reproduce report, read the attempt artifacts and controls against the trigger it tried. | Pass when the shown artifacts directly support the stated result: they demonstrate the issue's distinctive behavior, or they document a faithful attempt that did not reproduce it. Fail when there is no artifact, the artifact only shows setup or normal operation, or it shows an adjacent error or symptom rather than the issue's behavior. A confident assertion is not an artifact. | required |
| Honest conclusion | Compare the claim comment and report's result, expected/actual statements, causal language, and generalizations with the shown artifacts, controls, and acknowledged environment differences. | Pass when the words claim no more than the evidence supports. A clearly labeled, evidenced cannot-reproduce passes when it states what was tried, what happened, and relevant differences or limitations. Fail when the package calls a different symptom a reproduction, reverses expected and actual behavior, claims an unshown root cause, generalizes beyond tested environments, or presents uncertainty as certainty. | required |
| Claim quality | Read the claim comment against the issue title/body and the work the author actually proposes next. | Pass when the comment identifies the specific issue behavior or investigation target and makes a concrete, modest commitment to reproduce or investigate and report back. It may mention an already completed reproduction only when that work is actually included. Fail when it is an interchangeable assignment request or `+1`, promises a guaranteed fix or completion date, claims unsupported work, or asks to reserve the issue without issue-specific intent. | required |
| Convention compliance | Read the repo-facts block's bug-report template and contribution policy, including linked AI-use rules, then inspect the candidate claim comment and repro report for every condition that applies to issue comments. In live mode, use the same files or templates in the repository and the draft comments. | Pass when the outgoing comments satisfy all stated conditions that apply to them, including required AI-assistance disclosure with the requested tool/extent detail. In eval mode, treat candidate packages as AI-assisted course work only when applying an explicit disclosure rule: if the policy requires disclosure for all AI use or for issues/comments, missing disclosure fails. Do not infer that a natural, issue-specific comment violates an own-words rule merely because the eval package is AI-assisted. Silence about AI passes when the repo states no disclosure requirement for issue comments, and a policy that requires disclosure only in code contributions or pull requests does not impose it here. Fail when an applicable required disclosure or other explicit comment/report convention is missing or contradicted. | required |

## Verdict rule

Grade every applicable check as `pass`, `fail`, or `unclear`.

Accept if and only if every required check passes. Reject if any required
check fails or is unclear; `unclear` counts as fail because a package whose
evidence cannot be verified is not ready to post. Name every failed or
unclear required check in the summary.

In live claim-only mode, apply the skill's claim-only rule: grade `Claim
quality` and `Convention compliance`, report the four repro-dependent checks
as not yet applicable, and leave those four checks out of the verdict.

Judge outcomes rather than formatting. Do not fail a report merely because it
is short, uses different headings, tests a newer version while acknowledging
the difference, or honestly cannot reproduce the bug. Do not pass one merely
because it is detailed, polished, or confident.
