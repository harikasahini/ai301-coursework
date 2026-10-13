# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diff-matches-plan | The changed files and behavior changes in the diff, read against the plan's files, scope, approach and Deviations | Every changed file and behavior change is named in the plan, recorded under Deviations, or openly named in the description as a difference from the plan. Every change the plan promises that is missing from the diff is likewise disclosed. A difference that appears only in the diff fails. | required |
| tests-match-plan | The test evidence, read against the plan's test plan and the runnable checks the repo's template or contributing guide names | Accept if the evidence demonstrates the planned behavior through before-and-after results, relevant regression tests, or credible test-suite results. Missing full command output alone is not a failure if the test result is reported; failed or unavailable checks pass when the reason is explained. | required |
| claims-match-diff | The title, description, summary, changes list and checklist, read against the diff | Every change in the diff has a matching entry. No entry or checklist item describes something the diff does not contain (a test, a file, a behavior). Any statement that the PR follows the plan is true of the diff. The issue it closes is the issue the plan targets. | required |
| diff-free-of-debris | The diff and the commit list | No debug lines, commented-out code, edits unrelated to the fix (including refactors or reformatting of lines the fix does not need), or committed scratch files. | required |
| repo-standards-met | The description, branch name and commits, read against the repo's stated PR template, contributing guide and AI policy | Every section and checklist item the template asks for is filled with real content. A box is ticked only where the evidence supports it. An AI-use disclosure is present in the author's own words if the repo's policy or the scope's house rules ask for one. Branch and commit names follow the stated convention. A repo that states no such ask requires none. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. An `unclear` grade counts as a fail.