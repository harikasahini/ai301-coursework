# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-matches-evidence | The plan's stated cause, read against what the repro evidence's traceback, output, or artifacts actually show | The plan names a cause that the repro evidence supports or directly points to; a cause that contradicts the evidence, or that the evidence is silent on, fails | required |
| scope-bounded | The plan's stated scope (what it will and won't change) and the files it names | The change is one bounded fix reachable from the diagnosis; it does not grow into unrelated files, a refactor, or a second problem the issue didn't ask about | required |
| stranger-executable | The plan's approach and file list | A stranger could start making the change from what's written, without having to guess which function or line, or invent missing steps | required |
| test-plan-observable | The plan's test plan, read against the repro evidence's steps | The test plan re-runs (or adapts) the repro evidence's own steps and states what observable output should change from before to after; a test plan with no before/after or no concrete command fails | required |
| honest-about-unknowns | The plan's risks/unknowns section, read against its diagnosis and approach | Genuine uncertainty is stated as uncertainty, not asserted as settled fact; a plan with no risks section when the diagnosis itself rests on an assumption fails | required |
| comment-respects-thread-and-conventions | The plan comment, read against the thread highlights and the repo-facts block's conventions | The comment doesn't ignore an open question or constraint raised in the thread, and follows the repo's stated conventions for a plan/approach comment | required |

## Verdict rule

Accept if every required check passes. Unclear counts as fail.
