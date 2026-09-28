# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Determine the mode before grading. In live mode, read `scope.md`
   first and stop exactly as `SKILL.md` requires if the repository is
   outside scope or the repo placeholder is unfilled. Then read
   `voice-guide.md`. In eval mode, do not read either file and do not
   fetch outside the bundle.
2. Read this procedure, then the full rubric and evidence guide. Make
   a worksheet with one row per rubric check and columns for evidence,
   grade, and reason. Do not grade a row yet.
3. Read the issue context before the candidate drafts. Record the
   requested behavior, explicit boundaries, relevant file or subsystem
   clues, and expected result. Also record maintainer directions,
   rejected approaches, requested tests, linked work, and policy facts.
4. Read the reproduction evidence next, before the plan can anchor the
   interpretation. Record environment, trigger and inputs, actual
   artifact, expected artifact, controls, and what each control rules
   in or out. In live mode this is the student's posted repro comment;
   on the house issue it is only the repro material quoted in the
   drafts.
5. Read the candidate plan once in full. Record its diagnosis, fix
   target, in-scope and out-of-scope work, files or areas, ordered
   approach, test steps and expected-after observations, risks,
   unknowns, and deviations.
6. Read the candidate plan comment last. Record what evidence,
   approach, test intent, thread direction, coordination, policy
   disclosure, certainty, and commitments it communicates. In live
   mode, separately note any quoted `voice-guide.md` rule it breaks.

This order keeps a polished plan from redefining what the issue and
reproduction actually established.

## Evidence gathering

1. Build a diagnosis record with three entries: the plan's exact
   causal claim; the repro fact or control supporting it; and any
   repro fact or control contradicting it. If the plan labels a
   hypothesis, also record the bounded validation and the decision it
   controls.
2. Build a scope record listing every proposed code, test,
   documentation, migration, UI, and cleanup change. For each item,
   mark whether the issue, causal fix, regression proof, or explicit
   maintainer direction requires it. Record every stated deferral.
3. Build an executability record containing the first named file or
   subsystem, the behavior to change there, the remaining ordered
   steps, and all choices postponed until implementation. Verify paths
   against repo facts or the live repository only when the package
   supplies enough information to do so.
4. Build a test record that pairs the before artifact with each
   expected-after artifact. Record the trigger or fixture, real code
   path, command or action, observable result, useful controls, and
   focused regression coverage.
5. Build an honesty record of unresolved causal, compatibility,
   performance, policy, and implementation facts. Beside each, record
   the plan's validation, fallback, deferral, or absence of handling.
   In a post-build live run, record the deviations statement.
6. Build a communications record from the complete thread and policy
   sources named by the evidence guide. List each material maintainer
   signal and whether the plan or comment engages it. Record linked
   work and coordination, applicable disclosure wording, prohibited
   promises, and, in live mode, voice-guide conflicts.
7. Put each fact into the worksheet row whose Evidence cell asks for
   it. Preserve short direct quotes for facts that will decide a fail
   or unclear grade.

## Check execution

1. Execute checks in rubric-table order. For each row, use only the
   sources named in that row and the corresponding gathered record;
   do not compensate for a failed condition with strength on another
   check.
2. Apply the pass condition literally to the outcome, not the length,
   headings, confidence, or polish of the drafts. Grade `pass` only
   when the named evidence establishes the condition. Grade `fail`
   when named evidence establishes a violation.
3. Grade `unclear` when evidence required to decide the condition is
   genuinely absent, mutually unresolved, or inaccessible in the
   allowed mode. Do not turn absence into a pass, invent repository
   facts, or fetch external evidence in eval mode. The special
   condition “no applicable policy” is a pass for policy compliance,
   not missing evidence.
4. Re-read a source only if the gathered record lacks a fact that the
   check's Evidence cell explicitly names. Otherwise grade from the
   worksheet so every check sees the same frozen facts.
5. For every grade, write one concise evidence line naming the
   deciding fact or quote. For an unclear grade, name exactly what is
   missing. Complete all rows even after one required check fails.
6. In live mode, report voice-guide conflicts in the readable summary
   with the violated rule quoted, but do not alter a rubric grade
   unless that same behavior also fails a rubric check.

## Verdict assembly

1. Apply the rubric verdict rule after every check has a grade:
   `accept` only if all required checks are `pass`; otherwise
   `reject`. Treat `unclear` on a required check as a hold and thus a
   rejection. Never let a preferred check change the verdict.
2. Before the machine output, print a short line per check with its
   grade and deciding evidence. For every failed or unclear required
   check, include the shortest direct quote or concrete absent fact
   that explains the hold. Add live-mode voice notes after the check
   lines when applicable.
3. Emit the fenced JSON object required by `SKILL.md`. Include every
   rubric check in table order, use only `pass`, `fail`, or `unclear`,
   and keep each evidence value to one line. Set `item` to the bundle
   id in eval mode or the issue URL in live mode.
4. Validate that the JSON verdict matches the required-check grades,
   that the fence is valid JSON, and that no text follows the closing
   fence.
