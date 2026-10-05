# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the issue context first: title, body, and labels, to know what behavior is being reported.
2. Read the repro-evidence block second: the accepted reproduction this plan must build from. Note the exact behavior it pins down (the error, the trigger, the code path), since the diagnosis check reads the plan against this, not against the issue alone.
3. Read the thread highlights third, noting any open question, constraint, or maintainer comment a plan comment should not ignore.
4. Read the repo-facts block fourth: bug-report/plan-comment template asks and the contribution policy, including any AI-use disclosure requirement.
5. Read the candidate plan in full, then the candidate plan comment, last. Reading the evidence before the plan prevents grading the plan's confidence instead of its correctness.

## Evidence gathering

1. For `diagnosis-matches-evidence`: pull the plan's stated cause (usually under a "Diagnosis" or "Root cause" heading) and the specific behavior/traceback/output named in the repro-evidence block. Record both as short quotes.
2. For `scope-bounded`: pull the plan's stated scope (what it will and won't touch) and its file list. Record the files named and any explicit "won't touch" statement.
3. For `stranger-executable`: pull the plan's approach section. Record whether it names specific functions, files, or lines, or only describes the problem in general terms.
4. For `test-plan-observable`: pull the plan's test plan and the repro-evidence block's steps. Record whether the test plan reuses or adapts those steps, and whether it states a concrete expected output change.
5. For `honest-about-unknowns`: pull the plan's risks/unknowns section and compare it against any assumption the diagnosis rests on. Record whether that assumption is named as a risk or stated as settled fact.
6. For `comment-respects-thread-and-conventions`: pull the plan comment's text, the thread highlights, and the repo-facts block's conventions. Record any thread point the comment doesn't address and any convention it doesn't follow.

## Check execution

1. Execute checks in this order: `diagnosis-matches-evidence`, `scope-bounded`, `stranger-executable`, `test-plan-observable`, `honest-about-unknowns`, `comment-respects-thread-and-conventions`. Earlier checks establish facts (the real cause, the real scope) that later checks depend on.
2. Grade each check using only the evidence recorded for it in the gathering stage; do not re-read the whole package per check.
3. If the evidence named for a check is genuinely absent from the package (not merely terse), grade that check `unclear`, with the evidence line stating what's missing, not a guess at what it might have meant.
4. A check's grade does not change based on another check's grade; grade each on its own stated pass condition, even if an earlier check already failed.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required check passed; preferred checks never change the verdict (none are currently preferred in this rubric).
2. Treat `unclear` as `fail`, per the rubric's stated rule.
3. In the output, quote the single piece of evidence that most directly decided the verdict, normally the first required check that failed, or, if all passed, the diagnosis evidence that confirms the plan is sound.
