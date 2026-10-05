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

harikasahini

**Plan comment**

[comment-link](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5987998201)

Plan for a fix on #72: `verify_password` catches passlib's identity failure instead of letting it propagate.

Root cause (confirmed in my repro above): the function is an unguarded pass-through to `pwd_context.verify(...)`, so a malformed stored hash raises `passlib.exc.UnknownHashError` instead of returning `False`.

Plan: catch `UnknownHashError` specifically and return `False`, remove the H-05 xfail marker once the test passes.

On scope: I'm keeping this narrow rather than also catching `ValueError` for the truncated-bcrypt case. @sseid4 proposed catching both and asked maintainers whether to narrow it, that's still unanswered. Narrowing here means the truncated-bcrypt case keeps producing a 500 at login, per @sseid4's finding. PR #78 (open) makes essentially the same change but catches both exception types, full overlap with this plan on the core edit, differing only in catch width. I don't have a strong reason to prefer narrow over #78's
broader version beyond minimalism; happy to defer to #78's approach if that's what maintainers want.

Checked for other callers: only api/routes/auth.py's login check, unaffected either way.

---

## Your branch

**Branch**

fix/72-verify-password-test

**Evidence**

Before (Unit 2 reproduction, re-confirmed at the start of Unit 3 on the
unfixed code):

    $ python3.11 -m pytest tests/unit/test_security.py -k "test_verify_with_wrong_hash_format" -v
    tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format XFAIL (issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False...) [100%]
    ==================== 24 deselected, 1 xfailed, 2 warnings in 0.40s ====================

    $ python3.11 -c "
    from core.security import verify_password
    result = verify_password('password', 'not_a_valid_bcrypt_hash')
    print(result)
    "
    Traceback (most recent call last):
      ...
      File ".../core/security.py", line 37, in verify_password
        return bool(pwd_context.verify(plain_password, hashed_password))
      ...
    passlib.exc.UnknownHashError: hash could not be identified

After (same commands, run against the built fix on this branch):

    $ python3.11 -m pytest tests/unit/test_security.py -k "test_verify_with_wrong_hash_format" -v
    tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED
    ==================== 1 passed, 24 deselected, 2 warnings in 0.17s ====================

    $ python3.11 -c "
    from core.security import verify_password
    result = verify_password('password', 'not_a_valid_bcrypt_hash')
    print(result)
    "
    False

Full regression check, same branch, after the fix:

    $ python3.11 -m pytest tests/unit/test_security.py -v
    ==================== 25 passed, 2 warnings in 4.65s ====================

All 25 tests in the file pass, including the 24 pre-existing `verify_password`
tests plus the now-passing H-05 test, confirming no regression from the
`UnknownHashError` catch.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Smoke run (--limit 3, --include-calibration): 2/3 scored items agreed (pkg-02
briefly disagreed, confirmed as run-to-run grading noise on an isolated
--only re-run, not a rubric defect).
Full run (final): 18/20 scored items, bar met (18/20: PASS), every category
matched (clear-accept 5/7, scope-creep 4/4, thread-convention 2/2, unbuildable
3/3, wrong-cause 4/4). This matches the agreement line in the committed
eval-run.txt.

**Package analysis**

pkg-02 (clear-accept, sharkdp/bat#3844): my rubric's verdict is accept; the
gold label is accept (agree). I'm naming this one because it briefly showed a
false reject in an earlier --limit 3 run (failed checks: diagnosis-matches-evidence,
honest-about-unknowns), which did not reproduce when I re-ran the same package
in isolation with --only pkg-02 immediately after — all six checks passed
cleanly on that re-run, matching gold. I read this as grading variance under
parallel workers rather than a rubric defect: by hand, the plan's diagnosis
("cursor overshoots cursor_max... background fill subtracts past zero") is
directly supported by the repro evidence's own timing tests (26.4s with
highlighting versus 0.3s without, with and without the pager in the loop), and
the plan's stated risk ("other underflow-prone width arithmetic may exist
outside print_line... I will grep and note anything suspicious") is a genuine,
honestly-flagged unknown. I did not change the rubric in response to this,
since the isolated re-run confirmed the checks were already reading the
package correctly.

**Check rationale**

"diagnosis-matches-evidence | The plan's stated cause, read against what the
repro evidence's traceback, output, or artifacts actually show | The plan
names a cause that the repro evidence supports or directly points to; a cause
that contradicts the evidence, or that the evidence is silent on, fails |
required"

I wrote this check to require the diagnosis to be checked against the
reproduction's own evidence, not merely to require that a diagnosis exists. My
group's in-class sample rubric only required "the plan says what causes the
bug," with no comparison step. Hand-grading calib-03 against that weaker
wording showed the gap directly: a plan whose stated cause (a pager
key-binding defect) was contradicted by the repro evidence's own test (a
26.4s slowdown that occurs even with no pager in the loop at all, pointing at
highlighting computation instead) still passed the sample check, because the
check never asked the evidence to be consulted. My version closes that gap by
making the pass condition explicitly comparative.

**Trade-offs**

I confirmed this check's comparative wording against both calibration
packages before trusting it on the scored set: calib-03's plan (gold: hold)
correctly fails diagnosis-matches-evidence, since its stated cause
contradicts the repro evidence's no-pager timing test; calib-01's plan (gold:
ready) correctly passes, since its stated cause matches exactly what the repro
evidence demonstrates. What this check accepts that a looser version might
reject: a terse diagnosis is fine as long as it's supported, the check never
penalizes brevity. What it still risks missing: a diagnosis that is merely
consistent with the repro evidence without being the only cause consistent
with it, since the check asks whether the evidence supports the stated cause,
not whether it rules out every alternative. I accept that gap, since ruling
out every alternative cause is a much higher bar than this rubric's other
checks (stranger-executable, test-plan-observable) are designed to carry
instead.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
