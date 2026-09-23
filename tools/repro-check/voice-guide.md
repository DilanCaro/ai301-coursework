# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a student developer making an early open-source contribution. I am
comfortable debugging and testing, but I am still learning this repository.
Readers can expect me to separate what I observed from what I suspect and to
report back with evidence.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

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

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- Guaranteed fixes, completion dates, merges, or requests to reserve an issue.
- Generic praise, exaggerated deference, or assignment boilerplate instead of
  issue-specific intent.
- "Same as above" or "can confirm" without my own environment, steps, and
  evidence.
- A root-cause claim, broad generalization, or reproduction claim that my
  artifacts do not support.
- Hidden AI assistance when the repository requires disclosure.
