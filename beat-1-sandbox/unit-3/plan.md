# Plan for issue #72: fail closed on unrecognized password hashes

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

## Diagnosis and evidence

My Unit 2 reproduction used passlib 1.7.4 and bcrypt 4.3.0 on commit
`f89c06fc3ff292df2a04a39ac51319d32a76b779`. Running

```bash
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --runxfail
```

through the real test path failed at `core/security.py:37`:

```text
return bool(pwd_context.verify(plain_password, hashed_password))
E   passlib.exc.UnknownHashError: hash could not be identified
```

The existing test passes `"not_a_valid_bcrypt_hash"` as the stored hash and
expects `verify_password("password", "not_a_valid_bcrypt_hash")` to return
`False`. Instead, `pwd_context.verify(...)` cannot identify a hash scheme and
raises `UnknownHashError`, which `verify_password` currently does not catch.
The first reproduction command reports the case as `XFAIL` only because the
test is marked `xfail(strict=True)` for issue #72 / manifest H-05.

## Scope

In scope:

- Update `verify_password` in `core/security.py` to catch
  `passlib.exc.UnknownHashError` from the existing
  `pwd_context.verify(...)` call and return `False`.
- Remove the issue #72 / H-05 `xfail` marker from
  `test_verify_with_wrong_hash_format` in `tests/unit/test_security.py`.
- Re-run the focused malformed-hash test and existing valid-hash controls.

Not in scope:

- Changes to password hashing, JWT creation or decoding, dependency versions,
  authentication routes, or unrelated security utilities.
- Broad exception handling around password verification.
- Handling malformed values that raise exception types other than
  `UnknownHashError`; my accepted reproduction established only the
  unrecognized-scheme case named by issue #72.
- Cleanup or refactoring outside the two files named by the issue.

## Files and areas

- `core/security.py`: import `UnknownHashError` from passlib and narrowly
  handle it inside `verify_password`.
- `tests/unit/test_security.py`: remove the strict `xfail` marker from the
  existing H-05 test; retain its assertion that the result is `False`.

## Approach

1. Add the specific passlib `UnknownHashError` import in `core/security.py`.
2. Wrap only the existing `pwd_context.verify(...)` call in
   `verify_password` with `try/except UnknownHashError`. Preserve its existing
   Boolean result for recognized hashes and return `False` only when passlib
   cannot identify the stored hash format.
3. Remove the `pytest.mark.xfail` decorator associated with issue #72 from
   `test_verify_with_wrong_hash_format`. Do not weaken or replace the existing
   assertion.
4. Run the focused test and the existing correct-password and wrong-password
   tests, then run the security unit-test file. If those pass, run the
   repository's required checks that apply to the change.

## Test plan

Use the same Python 3.11 virtual environment and dependency versions recorded
in the Unit 2 reproduction.

1. Before the change, retain the Unit 2 result:

   ```bash
   pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --runxfail
   ```

   Expected before: `FAILED` with
   `passlib.exc.UnknownHashError: hash could not be identified`.

2. After the change, rerun the focused test without bypassing markers:

   ```bash
   pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv
   ```

   Expected after: `PASSED`, not `XFAIL` or `XPASS`, because the marker has
   been removed and `verify_password(...)` returns `False`.

3. Rerun the direct trigger through the changed function:

   ```bash
   python -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"
   ```

   Expected after: the command prints `False` and exits successfully without a
   traceback.

4. Preserve recognized-hash behavior:

   ```bash
   pytest \
     tests/unit/test_security.py::TestSecurity::test_verify_password_correct \
     tests/unit/test_security.py::TestSecurity::test_verify_password_incorrect \
     -vv
   ```

   Expected after: both tests pass, showing that a correct password still
   returns `True` and a wrong password against a recognized hash still returns
   `False`.

5. Run the containing test file:

   ```bash
   pytest tests/unit/test_security.py -vv
   ```

   Expected after: the file passes with no failure, `XFAIL`, or strict
   `XPASS` for H-05. Then run the repository-required checks:
   `make lint`, `make typecheck`, and `make test-unit`.

## Risks and unknowns

- Catching too broad an exception could conceal programming errors or
  dependency failures. The plan therefore catches only `UnknownHashError`,
  which is the exception demonstrated by my reproduction and named by the
  issue.
- Other malformed strings may cause passlib to raise a different exception.
  My own accepted reproduction did not establish those cases, so broadening
  behavior speculatively is out of scope. I will record any such finding
  separately rather than silently widening this fix.
- passlib 1.7.4 and bcrypt 4.3.0 print unrelated deprecation/version warnings
  in this environment. Those warnings appeared independently of the
  `UnknownHashError` and are not a success or failure signal for this change.
- Several classmates are working on the same classroom issue. Under the Path
  Review house rules their plans do not block mine; this plan and its evidence
  are independently stated from my own reproduction.

## Thread coordination

PR #75 is open and linked from issue #72. It implements the same fail-closed
outcome and removes the H-05 `xfail` marker, but it catches `ValueError` based
on additional malformed-input evidence that was not part of my accepted Unit
2 reproduction. Its author reports green CI.

I will not copy or present PR #75's work as mine. The Path Review house rules
still require me to build my independently evidenced plan on my own fork, so
I will keep my course branch limited to the `UnknownHashError` case my
reproduction established. Before any pull request is opened in Unit 4, I will
re-check PR #75. If it remains open, I will link it and explicitly ask whether
my narrower implementation or regression evidence is useful rather than
asking maintainers to choose silently between duplicate fixes. If PR #75
lands first, I will rebase and will not submit a duplicate production change;
I will retain only nonduplicative test evidence or follow the instructor's
house-issue direction. This lets me complete the required branch work without
racing or ignoring the existing pull request.

## Draft plan comment

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

## Deviations

The implementation followed the accepted plan without deviation. It catches
only `passlib.exc.UnknownHashError` around the existing
`pwd_context.verify(...)` call, returns `False` for the reproduced malformed
hash, and removes only the H-05 `xfail` marker. No broader exception handling,
dependency changes, refactors, or unrelated security changes were added. The
focused test, direct trigger, valid-hash controls, complete security test
file, and full unit suite passed. The warnings printed by the suites were
pre-existing Pydantic, Python `crypt`, and unrelated `AsyncMock` warnings, so
they did not justify changing the implementation or expanding the plan.
