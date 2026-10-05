# Plan: fix #72, verify_password raises UnknownHashError on malformed stored hashes

## Diagnosis

As confirmed in my Unit 2 reproduction (https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5878511933):

> `verify_password` (`core/security.py:37`) is a one-line pass-through
> to `pwd_context.verify(...)` with no exception handling, so passlib's
> error propagates instead of being caught and returned as `False`.

The repro confirmed this on Python 3.11 (the repo's targeted version), passlib 1.7.4, commit 2f4e82f: calling `verify_password("password", "not_a_valid_bcrypt_hash")` raises `passlib.exc.UnknownHashError: hash 
could not be identified` from inside passlib's `_identify_record`,
rather than returning `False`. The existing test `test_verify_with_wrong_hash_format` (manifest H-05) is marked
`@pytest.mark.xfail(strict=True)`, pinning exactly this behavior as the known bug.

## Scope

In scope: catching the identification failure inside `verify_password` and returning `False`.

Not in scope: any other function in `core/security.py`, the hashing scheme, and hash storage/migration. I am keeping the catch narrow (`UnknownHashError` only) rather than also catching `ValueError` for the truncated-bcrypt case (`'$2b$12$abc'`, which several repro reports show raising `ValueError: salt too small`). This is a provisional choice, not a settled one: @sseid4 proposed catching both exception types and asked maintainers whether to narrow it; that question is still unanswered. I'm narrowing for this PR so the change stays minimal and traceable to this issue's specific exception, but I want to be upfront that this leaves the truncated-bcrypt case unresolved, including @sseid4's finding that it currently turns the login endpoint's 401 into a 500.

PR #78 (open) makes essentially the same change with the broader catch, `(UnknownHashError, ValueError)`. The two overlap fully on the return-line edit and the xfail removal; catch width is the only difference.

## Files

- `core/security.py` (the fix: wrap `pwd_context.verify(...)` to catch the identification failure)
- `tests/unit/test_security.py` (remove the `strict=True` xfail marker from `test_verify_with_wrong_hash_format` once the test passes, per CONTRIBUTING.md's instruction that removing the marker is part of fixing a seeded bug)

## Approach

1. In `core/security.py`, wrap the `pwd_context.verify(...)` call in `verify_password` in a try/except catching
   `passlib.exc.UnknownHashError`, returning `False` on that path, leaving the success path unchanged. Confirmed via
   `UnknownHashError.__mro__` that it inherits from `ValueError`, not a passlib-wide hash-error base, so the except clause targets `UnknownHashError` specifically rather than a broader class that could silently swallow unrelated `ValueError`s elsewhere in the call.
2. Run `test_verify_with_wrong_hash_format` to confirm it now passes instead of `xfail`-ing.
3. Delete the `@pytest.mark.xfail(...)` decorator and its `reason=` string from that test, since `strict=True` means CI fails with `XPASS(strict)` if the marker stays once the bug is fixed.
4. Run the full `test_security.py` suite to confirm no other test (including the 15 other `verify_password` tests already in the file) regresses.

## Test plan

Re-run my Unit 2 repro steps against the fixed code, on Python 3.11, and compare to the before:

python3.11 -m pytest tests/unit/test_security.py -k "test_verify_with_wrong_hash_format" -v


Before (Unit 2 and confirmed again today): reported `XFAIL`.
Expected after: reported `PASSED`, with the `xfail` marker removed.

python3.11 -c "
from core.security import verify_password
result = verify_password('password', 'not_a_valid_bcrypt_hash')
print(result)
"

Before (Unit 2 and confirmed again today): raised `passlib.exc.UnknownHashError: hash could not be identified`.
Expected after: prints `False`, no exception raised.

Also re-run the full `test_security.py` file (`python3.11 -m pytest tests/unit/test_security.py -v`) to confirm the
other 15 `verify_password` tests still pass, since the fix changes shared code in a function those tests also exercise.

## Risks and unknowns

- Resolved: grepped the repo for other callers of `verify_password` outside the test file. Found exactly one, `api/routes/auth.py:80`, used as a plain boolean in a login check.
- Open: whether the narrow catch is actually the right call. @kpoon72 and @akshay-sarkar already noted that a broad catch also turns `PasswordSizeError` (an oversized-password case) into `False`, and judged that acceptable, fail-closed on size seems reasonable for a login boolean. I don't have a stronger reason than theirs to prefer narrow; I'm choosing it mainly because it's the minimal change matching this specific issue, not because broad is wrong. A maintainer may prefer PR #78's broader version instead, in which case this plan should defer to it.

## Deviations

None. The implementation matched the plan: caught UnknownHashError specifically in verify_password, returned False, removed the H-05 xfail marker. No changes to scope or approach during the build.
