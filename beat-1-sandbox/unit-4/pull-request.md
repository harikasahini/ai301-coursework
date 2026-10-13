# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[PR-180](https://github.com/codepath/pathreview-ai301-fa26-s3/pull/180)

**Branch**

fix/72-verify-password-test

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1 (full): 13/20 scored items, below the bar (18/20). Seven clear-accept packages (pkg-02, pkg-05, pkg-08, pkg-11, pkg-13, pkg-16, pkg-19) failed on tests-match-plan alone.
Run 2 (full): 19/20 scored items, bar met (18/20: PASS), every category matched. pkg-11 still disagreed with gold on claims-match-diff.
Run 3 (full, final): 20/20 scored items, bar met (18/20: PASS), every category matched. This matches the agreement line in the committed eval-run.txt.

**Package analysis**

pkg-02 (clear-accept): my rubric's first verdict was reject, failed on tests-match-plan; the gold label is accept. My first wording of that check required each command in the plan's test plan to appear with its printed output."too many arguments". My check read that as no proof, even though the staff accepted the package. After I loosened the check, my rubric's verdict on pkg-02 became accept, matching gold, and it stayed accept in the final run.

**Check rationale**

"| tests-match-plan | The test evidence, read against the plan's test plan and the runnable checks the repo's template or contributing guide names | Accept if the evidence demonstrates the planned behavior through before-and-after results, relevant regression tests, or credible test-suite results. Missing full command output alone is not a failure if the test result is reported; failed or unavailable checks pass when the reason is explained. | required |"

I revised this after my first full run showed that every clear-accept miss came from this one check. The original asked for each command with its printed output, which is stricter than what the staff accepted. The new wording accepts credible before-and-after or regression results, and it passes a check that failed or could not run when the reason is stated, so an honest shortfall does not mean hold.

**Trade-offs**

Loosening a check can flip packages the staff rejected, so I looked at the category tallies after the change. The not-tested packages (pkg-04, pkg-07, pkg-10, pkg-14) still rejected, and both standards-wall packages still rejected, so the looser wording did not cost me those categories. What the check now gives up: it accepts a reported test result without raw output, so it cannot tell a real result from an invented one. I accept that miss because the other checks compare the diff and the description to the plan, and the rubric can only judge what the package shows. One more gap: my rubric never says when an AI-use disclosure applies, so when I ran it on my own PR it counted the disclosure as applying only because my draft included one. pkg-11 disagreed with gold at 19/20 on claims-match-diff and agrees at 20/20. I did not change claims-match-diff between those runs, so I do not know what moved it. It may be grading variance, or a result of the missing-input step I added to the procedure.

---

Relat
