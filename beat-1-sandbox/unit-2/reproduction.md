# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

DilanCaro

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5787937433

I’d like to investigate issue #72. I’ll reproduce how `verify_password` handles a malformed stored hash in a clean environment, record the relevant versions, commands, and output, and report my results here before proposing a change.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5788083972

### Environment

- OS: macOS 26.6.2 (Build 25G83)
- Python: 3.11.2
- passlib: 1.7.4
- bcrypt: 4.3.0
- pytest: 9.1.1
- Repository: `DilanCaro/pathreview-ai301-fa26-s1`
- Commit: `f89c06fc3ff292df2a04a39ac51319d32a76b779`
- Installation: editable install with development dependencies in a Python 3.11 virtual environment

### Steps to reproduce

From a clone of the repository:

```bash
/opt/local/bin/python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip setuptools wheel
python -m pip install -e ".[dev]"
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv -rxX
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --runxfail
```

The first pytest command reports the existing test as `XFAIL` with:

```text
issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
```

The second command uses pytest's `--runxfail` option to expose the underlying behavior
without editing the test or implementation.

### Expected behavior

`verify_password("password", "not_a_valid_bcrypt_hash")` returns `False`.

### Actual behavior

`verify_password` raises `passlib.exc.UnknownHashError` while passlib attempts to identify
the malformed stored hash:

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

This reproduces the behavior described in issue #72 on the recorded commit. The two
deprecation warnings printed by the test are unrelated to the `UnknownHashError`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

agreement: 19/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)

agreement: 2/2 scored items

agreement: 18/20 scored items  (bar: 18/20: PASS)

agreement: 20/20 scored items  (bar: 18/20: PASS)

**Package analysis**

I analyzed `pkg-13`. My rubric decided `reject`, and the gold label was also `reject`.

The candidate report asserted:

> Can 100% confirm this bug.

and:

> It happens every single time I have a long session going, guaranteed reproducible on my end.

However, it supplied no commands, measurements, DWM observations, or other artifacts
showing the claimed behavior. It also did not record the Windows build or Windows Terminal
version requested by the repository's bug-report template. My rubric therefore rejected it
under Environment fidelity, Followable reproduction, Behavior evidence, Honest conclusion,
and Claim quality. In particular, the certainty of “guaranteed reproducible” was unsupported
by evidence a reader could inspect.

**Check rationale**

My final rubric includes this check:

> `| Behavior evidence | Read the report's observable artifacts—terminal output, logs, measurements, screenshots described in text, generated output, or control results—against the issue's actual and expected behavior. For a cannot-reproduce report, read the attempt artifacts and controls against the trigger it tried. | Pass when the shown artifacts directly support the stated result: they demonstrate the issue's distinctive behavior, or they document a faithful attempt that did not reproduce it. Fail when there is no artifact, the artifact only shows setup or normal operation, or it shows an adjacent error or symptom rather than the issue's behavior. A confident assertion is not an artifact. | required |`

I wrote the check around observable behavior rather than confidence, report length, or
formatting. The operator-swap exercise showed that a polished report can display a real
artifact while still exercising the wrong behavior. The final wording therefore requires
the artifact to demonstrate the issue's distinctive behavior and explicitly says that an
adjacent error or confident assertion is insufficient. It also permits an evidenced,
faithful cannot-reproduce result because that can still provide useful and honest evidence.

**Trade-offs**

The Behavior evidence check rejects potentially truthful confirmations when the author did
not include an artifact that another reader can inspect. For example, `pkg-13` may describe
a bug the author genuinely experienced, but statements such as “Can 100% confirm this bug”
cannot establish that the observed lag matched the issue without measurements, output, or
documented observations. I accept that this can miss a real confirmation because the skill
is deciding whether a reproduction is ready to post, not whether the author's experience is
possible. Requiring shareable evidence reduces unsupported confirmations and wrong-target
reports.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
