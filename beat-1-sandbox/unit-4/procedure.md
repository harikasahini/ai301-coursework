# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

# Procedure: how this tool grades a PR package

## Read order

1. Before reading, confirm each input the request names exists. If one is missing (for example no plan.md, or the draft text sits in a different file than the one named), say which file is missing and where you found the nearest text, then grade each check that depends on it `unclear`. Do not treat another file as the plan.
2. Read the issue first: its title, body, and thread. Note the behavior it reports and any maintainer constraint on the fix.
3. Read the plan next, in full, including Deviations. List the files it names, its approach steps, its test plan commands, and each deviation. Read the plan before the diff because the diff is judged against it.
4. Read the diff. List every changed file and each behavior change. Flag anything that looks like debris: debug lines, commented-out code, edits to lines the fix does not need, files the plan does not name.
5. Read the test evidence. List each command run, its output, and any check that failed or did not run.
6. Read the PR title and description. List each entry in the changes list, each behavior claim in the summary, the issue number it closes, which template sections are filled, and whether an AI-use disclosure is present.
7. Read the repo's standards last: the PR template, contributing guide, and any AI policy. Note the required sections, the branch and commit naming convention, and any disclosure rule. They come last so the comparisons above are done before the standards frame them.

## Evidence gathering

1. For diff-matches-plan: pair the list of files in the diff with the files the plan names, and each behavior change with a plan approach step or a Deviation. Record every file or change with no match, and every plan promise with no matching change.
2. For tests-match-plan: pair each command in the plan's test plan with the same command in the test evidence, and confirm the output shows the change the plan predicted. Pair each runnable check the PR template or contributing guide names with an output in the evidence. Record any command or check with no output.
3. For claims-match-diff: pair each description entry and each summary claim with a hunk in the diff, and each hunk with a description entry. Compare the issue number after the closing keyword with the issue the plan targets. Record each unmatched entry or hunk.
4. For diff-free-of-debris: scan every hunk for debug lines, commented-out code, unrelated edits, whitespace-only or reformatting-only changes to lines the fix does not need, and scratch files. Record each one with its file.
5. Check each ticked box against the test evidence and the diff. Find any AI-use disclosure the repo's policy or the scope's house rules require and check it is present, in the author's own words. Compare the branch name and commit messages with the stated convention. Record each gap.
6. In live mode, gather the diff by running `git diff main...HEAD`, and the issue-side items from the thread and the repo files. In eval mode, take every one of these from the matching part of the bundle only.

## Check execution

1. Execute the checks in the order they appear in the rubric.
2. Grade each check only from the evidence recorded for it. Do not re-read the whole package for each check. Re-read a part only to resolve an `unclear`.
3. If the evidence a check needs is genuinely absent from the package (for example, no test evidence at all), grade it `unclear` and write what is missing in the evidence line. A claim in the description that evidence exists is not evidence.
4. Grade honest disclosure on the facts. A difference between diff and plan that Deviations or the description names openly is a recorded deviation, not drift. A check that failed and is reported with its reason is evidence, not a failure of the PR.
5. Grade each check on its own condition. Another check's grade never changes this one.
6. In live mode, after the last check, read `voice-guide.md` and hold the PR title and description against it. Record each broken rule in the summary. This step never changes a grade.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required check passed, and reject if any required check failed.
2. Treat each `unclear` as a fail, as the rubric states.
3. In the output, quote the evidence from the first failing required check in rubric order. If no check failed, quote the evidence from the diff-matches-plan check.
4. Emit one JSON entry per rubric check, in rubric order, and end the reply with the JSON block.