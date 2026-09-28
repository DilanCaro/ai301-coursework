# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

In an eval bundle, read the candidate plan's diagnosis beside the
repro-evidence block: environment, trigger, actual and expected
behavior, artifacts, and especially control runs. Use the issue and
thread only to add context; a confident thread claim cannot override a
control that rules it out. In live mode, use the diagnosis in
`plan.md`, the student's posted reproduction comment on the issue, and
the issue's current body and thread. On the house issue, only repro
evidence quoted into `plan.md` or `comment.md` is available to the
grader.

Good grounding identifies a cause or causal layer that explains the
distinctive artifact and survives the controls. If the evidence does
not isolate one cause, a good plan labels its best explanation as a
hypothesis and makes the first implementation step a bounded check
that will choose or reject it. A symptom restated as a cause, or a
cause contradicted by a control, is not grounding.

## Scope

In an eval bundle, compare the candidate plan's change, in-scope and
not-in-scope statements, files or areas, and approach with the issue
request, repro evidence, and relevant thread direction. In live mode,
use the same plan fields and compare them with the live issue and
thread.

Good scope is the smallest reviewable change that addresses the
reproduced cause, plus the focused tests needed to prove it. Every
named area contributes to that one outcome, while migrations,
redesigns, new options, adjacent UI work, and cleanup are deferred
unless the evidence makes them necessary. A long plan can be bounded,
and a one-line plan can still be broad.

## Executability

In an eval bundle, locate the candidate plan's named files or
subsystems, chosen approach, ordered changes, and any decision points;
check those against paths and conventions in the repo-facts block,
issue, and thread. In live mode, use `plan.md` and verify repository
facts in the issue-linked repository's current tree and contribution
documentation when necessary.

Good executability lets another contributor name the first code or
test location, the behavior to alter, and what follows. Limited
discovery is acceptable when it has a narrow target and a decision
rule. “Investigate,” “profile,” “fix upstream or locally,” or several
unchosen implementation layers leave the package unbuildable.

## Test plan

In an eval bundle, map each candidate test step to the repro-evidence
block's trigger, inputs, commands, actual artifact, controls, and
expected behavior. In live mode, map the test plan in `plan.md` to the
student's posted Unit 2 reproduction comment. If that repro used a
stand-in rather than the real code path, require the same inputs to be
turned into a check through the real changed path.

Good testing states the command or action, relevant input or fixture,
and observable expected-after result that would fail before and pass
after. It reruns the reproduced case and preserves a useful control or
regression test. A full suite is useful support but is not decisive by
itself; neither are “works,” “looks better,” or “should feel fast.”

## Honesty

In an eval bundle, read the candidate plan's risks, unknowns,
assumptions, alternatives, and the certainty used in both the plan and
comment against gaps in the repro and thread. In live mode, also read
the deviations section of `plan.md`; after implementation it must say
either what changed and why or, in the author's own words, that the
build did not deviate.

Good honesty separates observation from inference and pairs material
unknowns with a validation, fallback, explicit deferral, or question
for review. It does not require inventing risks when evidence is
conclusive. Bad honesty hides a major choice until build time, claims
an untested cause as certain, or lets the implementation depart from
the plan without recording the difference.

## Comms

In an eval bundle, compare the candidate plan and plan comment with
the thread highlights and the repo-facts block's bug-report,
contribution, and AI-use policies. Record explicit maintainer
directions, approaches already rejected, requested tests, prior art,
open or linked pull requests, and disclosures required in issue
comments. In live mode, read the complete current issue thread,
linked work visible there, and current contribution-policy files
(`CONTRIBUTING.md`, repository instructions, and any AI policy).
Apply `scope.md` house rules as well.

Good communication engages every material thread signal: it follows
the requested direction or explains why the evidence supports a
different bounded route, coordinates with existing work instead of
racing it, and presents the author's own plan rather than “same as
above.” It obeys policies exactly. Where disclosure is required, the
comment names the tool and extent of assistance and preserves human
responsibility; where no issue-comment disclosure is required, its
absence is not a failure. A good comment is issue-specific, makes no
deadline or merge guarantee, and briefly connects evidence, approach,
and verification.
