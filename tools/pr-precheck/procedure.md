# Procedure: how this tool grades a PR package

## Read order

1. Determine the mode before grading. In live mode, read `scope.md`
   first and stop exactly as `SKILL.md` requires if the repository is
   outside scope or the repo placeholder is unfilled. Then read
   `voice-guide.md`. In eval mode, do not read either file and do not
   fetch outside the bundle.
2. Read this procedure, then the full rubric and evidence guide. Make
   a worksheet with one row per rubric check and columns for evidence,
   grade, and reason. Do not grade a row yet.
3. Read the issue context and thread highlights first. Record the
   requested behavior, any explicit maintainer direction about the
   fix, and any linked prior art that the PR must engage.
4. Read the repo-facts block next (or, live, the PR template and
   contribution / AI policy). Record every required template section,
   checklist item, closes/fixes convention, changelog ask, and
   disclosure rule.
5. Read the plan-context block before opening the candidate PR. Record
   the plan's in-scope and not-in-scope commitments, named files or
   areas, test plan steps and expected-after observations, repro
   grounding, and any deviation or deferral notes. This freeze is what
   the diff and description will be graded against.
6. Read the candidate PR title and description next. Record what they
   claim changed, what they claim was deferred, any fidelity claim
   ("exactly as planned", "no changes beyond…"), and which template
   sections are filled.
7. Read the commit list, then the unified diff hunk by hunk. List every
   changed file and material behavior; mark debris, unrelated edits,
   and anything outside the plan's boundary.
8. Read the test-evidence section last. Record before/after artifacts,
   which plan test steps they cover, whether the changed path was
   exercised, and whether repo checks are shown.

This order keeps a polished description from redefining what the plan
and diff actually contain.

## Evidence gathering

1. **Plan fidelity.** Build a scope-vs-diff record: list every planned
   deliverable and every deferred item; list every material change in
   the diff. Mark each diff change as in-plan, covered by a deviation
   note, or silent drift (more). Mark each still-claimed plan item as
   present, honestly deferred, or silently missing (less). Quote any
   description fidelity claim next to the mismatch it would conceal.
2. **Test evidence.** Build a test record that pairs each plan test
   step (and the plan-context repro) with the evidence shown. For each
   pair, record the command or action, whether it hits the changed
   path, the before artifact, the after artifact, and whether the
   expected-after is observable. Separately record the repo-suite or
   check outcome, or the honest failing-check note.
3. **Diff quality.** Build a debris record from the diff and commits:
   debug prints, commented-out experiments, dead helpers, TODO litter,
   pure formatting/import churn, drive-by files, and commit subjects
   that advertise WIP or cleanup-as-substance.
4. **Standards and comms.** Build a compliance record listing each
   repo-facts template ask and AI-disclosure rule, and whether the
   description meets it with real content. Note blank, boilerplate, or
   missing required sections.
5. Put each fact into the worksheet row whose Evidence cell asks for
   it. Preserve short direct quotes for facts that will decide a fail
   or unclear grade.

## Check execution

1. Execute checks in rubric-table order. For each row, use only the
   sources named in that row and the corresponding gathered record;
   do not compensate for a failed condition with strength on another
   check.
2. Apply the pass condition literally to the outcome, not the length,
   headings, confidence, or polish of the PR text. Grade `pass` only
   when the named evidence establishes the condition. Grade `fail`
   when named evidence establishes a violation.
3. Grade `unclear` when evidence required to decide the condition is
   genuinely absent from the allowed world. Do not invent repository
   facts or fetch external evidence in eval mode. "No applicable
   policy / no applicable template ask" is a pass for that part of
   Template and disclosure, not missing evidence.
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
   grade and deciding evidence. When quoting the deciding failure,
   quote the first failing or unclear required check in rubric-table
   order; if several failed, still name that first one as the
   deciding check and list the others in the summary.
3. Emit the fenced JSON object required by `SKILL.md`. Include every
   rubric check in table order, use only `pass`, `fail`, or `unclear`,
   and keep each evidence value to one line. Set `item` to the bundle
   id in eval mode or the PR / issue URL in live mode.
4. Validate that the JSON verdict matches the required-check grades,
   that the fence is valid JSON, and that no text follows the closing
   fence.
