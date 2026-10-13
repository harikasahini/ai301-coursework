# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

- In a practice submission: "Plan context" (the plan's Files list, scope, Not in scope, test plan, and any Deviations), read against "Candidate PR": the Diff (every file header and hunk) and the Description.
- In my own PR: plan.md (files, approach, `## Deviations`) against `git diff main...HEAD` and pr_draft.md.
- Good looks like: every changed file and behavior change is named in the plan, recorded under Deviations, or openly named in the description. Every promised change that is missing is disclosed. No sentence claims the PR follows the plan when the diff does more or less.

## Test evidence (harness category: not-tested)

- In a practice submission: "Test evidence" under "Candidate PR", read against the test plan in "Plan context" and the template or checklist asks in "Repo facts".
- In my own PR: test_evidence.md against the test plan in plan.md and the checks the PR template lists.
- Good looks like: each command appears with its printed output, and the output shows the change the plan predicted (before and after). A sentence, or a note after `#` saying what it printed, is not proof. A check that failed or could not run, reported with its reason, counts as evidence.

## Diff quality (harness category: unreviewable)

- In a practice submission: the Diff and Commits under "Candidate PR".
- In my own PR: `git diff main...HEAD`, `git log main..HEAD --oneline`, and `git status` for scratch files.
- Good looks like: every hunk serves the fix. No debug lines, commented-out code, unrelated refactors or reformatting, or committed scratch files, and each hunk traces to the plan.

## Standards and comms (harness category: standards-wall)

- In a practice submission: the "pull requests" and "contribution policy" lines in "Repo facts" (template asks, checklist items, any AI policy), read against the Title, Description (including its Checklist) and Commits under "Candidate PR".
- In my own PR: .github/PULL_REQUEST_TEMPLATE.md, docs/CONTRIBUTING.md and scope.md's house rules, against pr_draft.md, the branch name and commit messages.
- Good looks like: every ask the repo states is met with real content, and boxes are ticked only where the evidence supports them. An AI-use disclosure appears in the author's own words where the repo or scope asks for one. Naming conventions are followed. A repo that states no AI ask requires none.
