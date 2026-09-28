# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Evidence-grounded diagnosis | Read the candidate plan's stated cause against the repro-evidence block's observed failure, controls, and expected behavior. In live mode, use the diagnosis in `plan.md` and the student's posted reproduction comment on the issue, or the repro quotations included in the drafts for the house issue. | Pass when the proposed cause explains the distinctive observed behavior and is not contradicted or ruled out by a control or artifact. Fail when the plan ignores stronger causal evidence, merely repeats the symptom as a cause, or names a cause that the package's own evidence rules out. | required |
| Causal fix target | Read the plan's proposed change and files or areas against the grounded diagnosis and the evidence that isolates the failure. | Pass when the change acts on the demonstrated or still-plausible cause at the relevant code path. A plan may preserve an explicitly stated hypothesis when the evidence cannot isolate one cause, but it must include a bounded validation step before committing to the fix. Fail when it only masks a symptom, chooses an evidence-contradicted layer, or proceeds with an untested guess as certainty. | required |
| Bounded scope | Read the plan's in-scope and not-in-scope commitments, named files or areas, and proposed work against the issue request, repro evidence, and any thread direction. | Pass when the work forms one reviewable change needed for the issue and explicitly defers unrelated refactors, migrations, features, or while-in-the-area cleanup. Multiple files or tests may pass when each is necessary to the same outcome. Fail when the fix is bundled with a redesign or adjacent work that can be omitted without weakening the fix. | required |
| Executable approach | Read the plan's files or areas, ordered approach, and unresolved implementation choices against the repo-facts block and issue context. | Pass when a contributor unfamiliar with the draft could identify where to start, what behavior to change, and the sequence or decision rule for doing it without first asking the author to choose among major layers or approaches. Exact line numbers are not required. Fail when investigation, profiling, or “fix whatever is found” substitutes for a chosen bounded implementation path. | required |
| Decisive test plan | Read the plan's test plan against the repro evidence's inputs, steps, controls, actual artifact, and expected behavior. | Pass when the plan reruns the relevant repro through the real changed code path, names an observable expected-after result, and includes a focused regression check or justified equivalent. Existing broader suites may supplement but not replace that check. Fail when success is only “works,” “feels faster,” “tests pass,” or another outcome that would not distinguish the fix from the reproduced failure. | required |
| Honest risks and unknowns | Read the plan's risks, unknowns, assumptions, alternatives, and deviation notes against unresolved facts in the issue, thread, and repro evidence. | Pass when material uncertainty is named and bounded by a validation, fallback, deferral, or review question, and when completed work does not silently contradict the stated plan. Also pass when the evidence leaves no material unknown and the plan makes no unsupported certainty claim. Fail when an unresolved cause, compatibility question, performance cost, or build-time choice is presented as settled or silently deferred to implementation. | required |
| Thread alignment | Read the plan and plan comment against explicit maintainer requests, rejected approaches, prior art, linked or open pull requests, and house rules in the issue context or live thread. | Pass when the package acknowledges and follows explicit direction, or clearly explains a bounded reason to propose another route. Known linked work passes when the plan gives a concrete coordination or reuse path that avoids duplicate final work; the mere existence of an open pull request does not fail an otherwise aligned plan. With no relevant thread direction, pass when the comment remains specific to this plan. Fail when it ignores or contradicts a material maintainer signal, piggybacks on another person's plan, or knowingly duplicates linked work without coordination. | required |
| Contribution-policy compliance | Read the candidate plan comment against the repo-facts contribution and AI-use policy; in live mode, read the repository's current contribution-policy files identified by the evidence guide. | Pass when the comment satisfies every policy that applies at comment time, including naming the AI tool and extent of assistance when disclosure is required, and otherwise makes no prohibited representation. If the repository states no applicable policy, pass. Fail when a required disclosure or other explicit comment convention is absent. | required |
| Maintainer-readable comment | Read the candidate plan comment against the issue, repro evidence, and candidate plan. | Pass when it states the issue-specific observed grounding, proposed bounded direction, and how success will be checked in the author's own words, without guarantees, invented certainty, or a promised deadline. It may be terse and need not duplicate every plan detail. | preferred |

## Verdict rule

Accept only when every required check passes. Reject when any required
check fails or is unclear. Preferred checks appear in the output but
never change the verdict; an unclear preferred check is reported as
unclear.
