# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

DilanCaro

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5863703007

I reproduced issue #72 on Python 3.11.2 with passlib 1.7.4 and bcrypt
4.3.0. The H-05 test reaches `pwd_context.verify(...)` with
`"not_a_valid_bcrypt_hash"`, and passlib raises `UnknownHashError` because it
cannot identify the stored hash format; `verify_password` currently lets that
exception escape.

I plan to keep the change to the two files named by the issue: catch only
`UnknownHashError` around the existing verification call in
`core/security.py` and return `False`, then remove the strict `xfail` marker
from `test_verify_with_wrong_hash_format` without changing its assertion. I am
not planning broader exception handling or unrelated security cleanup.

I also saw the linked open PR #75, which implements the same outcome with a
broader `ValueError` catch based on additional malformed-input evidence. Per
the Path Review classroom rules, I will still build my independently grounded
branch on my fork, but I will not present or copy that PR's work as mine.
Before opening a pull request in Unit 4, I will re-check #75: if it is still
open, I will link it and ask whether my narrower implementation or regression
evidence is useful; if it lands first, I will not submit a duplicate
production change and will retain only nonduplicative test evidence or follow
the instructor's house-issue direction.

I will rerun the focused H-05 test and expect `PASSED` rather than `XFAIL`,
rerun the direct malformed-hash call and expect `False` with no traceback, and
run the existing correct- and wrong-password tests to confirm recognized
bcrypt hashes still return `True` and `False` as before.

---

## Your branch

**Branch**

`fix/72-malformed-hash`

https://github.com/DilanCaro/pathreview-ai301-fa26-s1/tree/fix/72-malformed-hash

**Evidence**

Before — Unit 2 reproduction on commit
`f89c06fc3ff292df2a04a39ac51319d32a76b779`, Python 3.11.2, passlib
1.7.4, bcrypt 4.3.0, and pytest 9.1.1:

```bash
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv -rxX
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --runxfail
```

The first command reported:

```text
XFAIL
issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
```

The second command exposed the underlying behavior:

```text
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format FAILED

>       result = verify_password("password", wrong_hash)

core/security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
...
E   passlib.exc.UnknownHashError: hash could not be identified

FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
======================= 1 failed, 2 warnings in 0.37s ========================
```

After — the same malformed-hash case through the changed code path:

```bash
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv
```

```text
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [100%]
======================== 1 passed, 2 warnings in 0.31s =========================
```

The test now passes normally rather than reporting `XFAIL` or
`XPASS(strict)`, confirming that the marker was removed and the assertion is
enforced.

The direct trigger from the reproduction now returns the expected value
without a traceback:

```bash
python -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"
```

```text
False
```

The recognized-hash controls remained unchanged:

```bash
pytest \
  tests/unit/test_security.py::TestSecurity::test_verify_password_correct \
  tests/unit/test_security.py::TestSecurity::test_verify_password_incorrect \
  -vv
```

```text
tests/unit/test_security.py::TestSecurity::test_verify_password_correct PASSED [ 50%]
tests/unit/test_security.py::TestSecurity::test_verify_password_incorrect PASSED [100%]
======================== 2 passed, 2 warnings in 1.35s =========================
```

The complete security test file also passed:

```bash
pytest tests/unit/test_security.py -vv
```

```text
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [ 88%]
======================== 25 passed, 2 warnings in 7.02s ========================
```

Finally, the repository unit suite completed successfully:

```bash
make test-unit
```

```text
=========== 376 passed, 52 xfailed, 3 warnings in 17.09s ============
```

The warnings were unrelated to this change: an existing Pydantic
class-configuration deprecation, Python's `crypt` deprecation inside passlib,
and an unrelated unawaited `AsyncMock` warning in
`test_list_reviews_counts_total`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. `agreement: 19/20 scored items  (bar: 18/20: PASS)`
2. `agreement: 4/4 scored items`
3. `agreement: 20/20 scored items  (bar: 18/20: PASS)`

The second run used `--only pkg-09,pkg-03,pkg-04,pkg-20` after revising
Thread alignment. The last score matches the confirming full run saved in
`eval-run.txt`.

**Package analysis**

I analyzed `pkg-09`. In my first full run, my rubric decided `reject`, while
the gold label was `accept`.

The candidate comment acknowledged the existing work:

> `I have read PR #2089, which takes the same route; if that lands first I will rebase my tests onto it rather than duplicate the change.`

My original Thread alignment check said a plan “must not race known work.”
The grader interpreted the candidate's intent to implement option 2 while
PR #2089 remained open as racing, even though the comment named the PR and
gave a reuse path if it landed. The gold label treated this as adequate
coordination: the plan was independently grounded, bounded, and explicit
about avoiding duplicate final work. I revised the check so the existence of
an open pull request alone does not fail a plan when it acknowledges the work
and states a concrete coordination or reuse path. The targeted rerun then
graded `pkg-09` as `accept`, matching gold.

**Check rationale**

My final rubric includes this check:

> `| Thread alignment | Read the plan and plan comment against explicit maintainer requests, rejected approaches, prior art, linked or open pull requests, and house rules in the issue context or live thread. | Pass when the package acknowledges and follows explicit direction, or clearly explains a bounded reason to propose another route. Known linked work passes when the plan gives a concrete coordination or reuse path that avoids duplicate final work; the mere existence of an open pull request does not fail an otherwise aligned plan. With no relevant thread direction, pass when the comment remains specific to this plan. Fail when it ignores or contradicts a material maintainer signal, piggybacks on another person's plan, or knowingly duplicates linked work without coordination. | required |`

I kept this check required because ignoring maintainer direction, rejected
approaches, or active linked work can make an otherwise technically strong
plan inappropriate to post. I revised the original absolute “must not race
known work” wording after `pkg-09` showed that it collapsed two different
cases: silently duplicating an open change and transparently coordinating
with it. The final wording still rejects plans that ignore or knowingly
duplicate linked work, while allowing a bounded plan that names the work and
explains how it will coordinate or reuse it.

**Trade-offs**

The revised Thread alignment check may accept two contributors planning the
same implementation while an earlier pull request is still open, as long as
the later plan states a credible coordination or reuse path. That creates
some risk of duplicated effort, but I accepted it because an open pull
request does not itself prove that work is reserved or will land.

I reran `pkg-03`, `pkg-04`, and `pkg-20` as canaries alongside `pkg-09`.
`pkg-03` remained an `accept` because it explicitly coordinated with prior
art and an open PR. `pkg-04` remained a `reject` because it ignored the
owner's active code-fix direction, and `pkg-20` remained a `reject` because
its required AI-use disclosure was absent. The canaries showed that the
revision corrected the `pkg-09` boundary without erasing the
thread-and-convention category.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
