# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: week 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; your operator swap showed you what that feels
like. Write the map you wish your executor had.
-->

## Environment

**Where it lives.** In an eval bundle, read the issue's versions,
platforms, configuration, and trigger conditions, then compare them with the
repro report's environment section and setup details. The repo-facts block
also lists the project's required bug-report fields. In live mode, use the
issue body and maintainer clarifications for the target, the repository's bug
report template for required fields, and the draft report for the attempted
environment.

**What good looks like.** The report records the details that could change the
result: relevant app/tool version, OS or platform, runtime/browser/backend,
installation or build form, and trigger-specific configuration. It either
matches the issue's target or calls out material differences and limits the
conclusion accordingly. A version number alone is insufficient when the issue
depends on a driver, build profile, browser language, shell, or similar
condition.

## Steps

**Where it lives.** In an eval bundle, use the issue's stated reproduction and
thread clarifications as the target, then inspect the repro report's setup,
commands/actions, pasted inputs, configuration, and controls. In live mode,
compare the GitHub issue and thread with the student's complete draft. Follow
links only when they are public and actually provide a needed input.

**What good looks like.** A stranger can move from an identified starting
state to the relevant trigger without guessing a material step. Exact command
counts or a required heading do not matter; complete state transitions do.
Private repositories, internal configuration, or omitted inputs make a report
unfollowable unless a shareable minimal substitute contains everything needed.
An operator, option, or action that changes the code path is not a harmless
variation.

## Behavior shown

**Where it lives.** In an eval bundle, locate terminal excerpts, logs,
measurements, generated output, screenshot descriptions, or control-run
results in the repro report. Read those artifacts beside the issue's expected
and actual behavior and any maintainer clarification. In live mode, use only
artifacts included in or publicly linked from the draft; an unshared local
file is not evidence a reader can inspect.

**What good looks like.** The artifact exposes the issue's distinguishing
behavior, not merely that the program launched or that some error occurred.
Exit status, error text, rendered output, ordering, or a control may be the
deciding signal. For a cannot-reproduce, the artifact should show a faithful
attempt and its observed non-trigger; that is useful evidence even though the
bug did not appear. Narrative certainty cannot replace observable output.

## Honesty

**Where it lives.** Compare the claim comment, the report's result and
expected/actual statements, and any root-cause or scope claims with the
artifacts, controls, environment record, and issue text. In live mode, also
check that statements about completed work are supported by the draft package
the student plans to post.

**What good looks like.** The conclusion stays inside the evidence. A
reproduction names the behavior actually shown; a cannot-reproduce says so
plainly, records the attempt, and identifies relevant limitations or
differences. Hypotheses remain hypotheses. A report is not honest evidence
when it renames an adjacent error as the bug, claims a cause without proof,
reverses expected and actual, or generalizes one environment to untested ones.

## Comms

**Where it lives.** In an eval bundle, compare the candidate claim comment
with the issue title/body and compare both candidate comments with the
repo-facts block's bug-report template and contribution policy. Read the exact
scope of any AI policy: some apply to all issues/comments, while others apply
only to code or pull requests. In live mode, inspect the repository's current
`CONTRIBUTING.md`, dedicated AI-policy files, `AGENTS.md`, issue template, and
linked contributor docs, then check the student's drafts.

**What good looks like.** The claim names the issue-specific behavior or
investigation and promises a realistic next action—investigate, reproduce,
test, and report back—not a guaranteed fix or deadline. Before reproduction,
it promises the report rather than pretending the result is known. The report
meets explicit repository asks that apply to an issue comment. When disclosure
is required, it names the tool and extent as requested; when policy is silent
or limits disclosure to pull requests, do not invent an issue-comment
requirement. A generic assignment request, `+1`, piggyback confirmation, or
unsupported certainty is not specific communication.
In eval mode, treat candidate packages as AI-assisted course work only when
applying an explicit disclosure rule. If the repository requires disclosure
for all AI use or for issues/comments, the disclosure must appear in the
candidate comment; absence fails. This eval assumption does not by itself
prove that a comment was AI-generated or not in the contributor's own words:
assess own-voice requirements from the text, and pass natural, issue-specific
comments unless the bundle supplies contrary evidence. If the policy has no
issue-comment disclosure requirement, or requires disclosure only for code or
pull requests, do not invent one.