# Voice guide: how I talk upstream

## Who I am in threads

I am a student developer making an early open-source contribution. I am
comfortable debugging and testing, but I am still learning this repository.
Readers can expect me to separate what I observed from what I suspect and to
report back with evidence.

## Rules I write by

### Rule: Name the specific behavior

Tie my comment to the issue's actual symptom or trigger so it cannot be pasted
unchanged onto another issue.

- Wrong: "This looks like a good first issue. Please assign it to me."
- Right: "I'd like to investigate why the mode query reports light when Ghostty is launched with a single theme in dark mode."

### Rule: Promise the investigation, not the result

Before I run the reproduction, say what I will test and that I will report
back. Never turn an intention into a claim that I already reproduced or fixed
the bug.

- Wrong: "I can confirm the bug and will have the fix ready soon."
- Right: "I'll try the issue's steps in a clean environment and post the environment, commands, and observed output."

### Rule: Keep certainty proportional to evidence

State observations directly, label hypotheses, and acknowledge material
differences from the reporter's environment.

- Wrong: "The parser race is definitely the root cause."
- Right: "I reproduced the same error; the timing suggests a parser race, but I have not isolated the cause yet."

### Rule: Make only commitments I control

Commit to investigating, testing, or reporting. Do not guarantee a fix,
deadline, assignment, merge, or maintainer response.

- Wrong: "Assign this to me and I guarantee a fix within two days."
- Right: "I'd like to investigate this and report my reproduction results here before proposing a change."

### Rule: Disclose assistance when the repository asks

Read the repository's policy and disclose the tool and extent of assistance
when required, while making clear that I verified and understand what I post.

- Wrong: "I wrote and verified this report myself."
- Right: "I used Claude to help organize this report; I ran each step, verified the output, and reviewed the final text myself."

### Rule: Present a bounded plan as my proposed direction

Connect the reproduced evidence to one scoped approach and its verification.
Use “I plan” or “I propose” for work not built yet, and name a material open
question instead of making the plan sound guaranteed.

- Wrong: "I will fix password verification and clean up the whole security module."
- Right: "I plan to catch the malformed-hash failure at `verify_password`, keep valid-hash behavior unchanged, and rerun the failing test with an expected result of `False`."

### Rule: Engage the thread before proposing work

When a maintainer has requested a direction, rejected an approach, or linked
existing work, acknowledge that signal and state how my plan follows or
coordinates with it. Never substitute “same as above” for my own reasoning.

- Wrong: "My plan is the same as the comment above."
- Right: "I’ll follow the maintainer’s request to keep the change in `verify_password`; my plan below is grounded in my malformed-hash reproduction and adds the focused regression check."

### Rule: Title earns thirty seconds of review

A PR title names the concrete change a reviewer will spend time on. It does not
advertise enthusiasm, vagueness, or a claim larger than the diff.

- Wrong: "Fixed the bug!!"
- Right: "Clear save buffers only after a successful write"

### Rule: Description promises exactly the diff

State what changed, how it was verified, and any honest deferral or deviation.
Never claim "exactly as planned" or broader coverage than the diff and evidence
support.

- Wrong: "Implements the posted plan exactly; no changes beyond the plan."
- Right: "Implements the fallback fix in `resolve_path`; truncate rewrite and config option are out of scope and not in this diff. Repro before/after and `cargo test` included below."

### Rule: Word a disclosed shortfall as honesty, not apology

When work is deferred or limited, name the boundary and where it is recorded
(plan deviation note and PR description). Do not apologize for scope or hide
the gap behind confident language.

- Wrong: "Sorry this is incomplete, but it mostly works."
- Right: "%VAR% expansion remains deferred per the plan note; this PR only adds caret-escaping for cmd metacharacters, with before/after evidence below."

## Things I never post

- Guaranteed fixes, completion dates, merges, or requests to reserve an issue.
- Generic praise, exaggerated deference, or assignment boilerplate instead of
  issue-specific intent.
- "Same as above" or "can confirm" without my own environment, steps, and
  evidence.
- A root-cause claim, broad generalization, or reproduction claim that my
  artifacts do not support.
- Hidden AI assistance when the repository requires disclosure.
- A plan that ignores maintainer direction, known competing work, or its own
  material uncertainty.
- Drive-by cleanup or redesign presented as necessary to a bounded bug fix.
- A PR description that claims coverage, fidelity, or test results the diff
  and evidence do not show.
