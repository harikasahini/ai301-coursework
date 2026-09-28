# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username:**
harikasahini

---

## Posted upstream

**Claim comment**

[Comment link](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5877417792)

Claiming this to investigate. From the issue, `verify_password` in `core/security.py` raises `UnknownHashError` when the stored hash is malformed, instead of returning `False` as the rest of the auth flow expects. There's an existing `@pytest.mark.xfail` test (H-05) that should define the target behavior once this is fixed.

I'll start by reproducing the crash from a malformed stored hash, confirm it against the H-05 test, and trace the call path to see where the exception should be caught. I'll report back with what I find, including my environment and the exact reproduction steps.

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1 (full): 18/20 scored items, bar met (18/20: PASS), every category matched
(clear-accept 6/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4).
Run 2 (full, final): 19/20 scored items, bar met (18/20: PASS), every category matched
(clear-accept 7/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4).
This matches the agreement line in the committed eval-run.txt.

**Package analysis**

pkg-05: my rubric's first verdict was reject; the gold label is accept. The failed check was
conventions-followed. The package (conda/conda#16543) is a strong reproduction: it isolates
the bug with a minimal env.yml, quotes the exact EnvironmentSectionNotValid output, and proves
the JSON stream breaks by piping through `python3 -m json.tool`. My original check read
"supplies what the stated template asks for," and the repo's bug-report template asks for the
output of `conda info` and `conda list`. The report gave a one-line environment summary instead
of raw command output, so the check failed it even though nothing about that omission weakened
the reproduction, since the reporter's own `conda info` was already in the issue and `conda list`
has no bearing on a stdout/stderr routing bug. I revised conventions-followed to ask whether the
comments give what's needed to evaluate this specific reproduction, rather than whether they
echo every field the template lists. After the fix, my rubric's verdict on pkg-05 became accept,
matching gold.

**Check rationale**

"conventions-followed | Both comments, read against the repo-facts block (stated bug-report
template asks and contribution policy) | The comments give what's needed to evaluate this
reproduction: environment or version info sufficient to place the bug, and any template field
materially relevant to it (not every field the template lists, if it doesn't bear on this bug).
If the repo's stated policy requires disclosing AI assistance, the comments disclose it; a
policy silent on AI use requires nothing. | required"

I revised this from a first version that failed a package (pkg-05) for not literally supplying
every field a bug-report template lists, even though the fields it skipped (raw `conda list`
output) had no bearing on the specific bug being reproduced. I rejected grading by template-field
completeness in favor of grading whether the comment gives a reader what they need to evaluate
that particular reproduction, since the rubric template itself warns against judging the
write-up's shape rather than the outcome.

**Trade-offs**

Before confirming this change with a full run, I re-ran it with `--only pkg-05,pkg-20` as a canary, since loosening conventions-followed could have let a package that
skips real disclosure requirements pass. Both packages graded correctly in that partial run
(pkg-05 flipped to accept, the disclosure package still agreed), and the confirming full run
held at 19/20 with disclosure still 1/1, so the looser wording did not cost me the one
disclosure-category package. What this version accepts is a report that omits a template field
if that field doesn't bear on the specific bug; what it still requires is that a disclosure
requirement, when the repo states one, is always relevant and must always be met.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
