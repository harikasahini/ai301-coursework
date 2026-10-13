---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question about one PR package: is this ready to submit? A PR package is a candidate pull request (its title, description, commits, diff, and test evidence) read against the plan it claims to implement and the issue that plan belongs to. Grade one package per run. Never answer a different question and never grade from gut feel. You answer by executing `rubric.md` and `procedure.md`, using `references/evidence-guide.md` to find the evidence.

## Inputs and modes

Run in exactly one of two modes. If the request names an issue URL and the student's own files, use live mode. If the request hands you a package bundle, use eval mode.

**Live mode** grades the student's own PR before it is opened. Read these inputs from the top folder of the student's fork clone, on their branch:

- `plan.md`, including its `## Deviations` section. A house-chain student reads the house plan instead.
- The diff: run `git diff main...HEAD` (three dots). It shows every committed change the branch makes relative to `main`. Uncommitted and untracked changes are not part of the PR, so do not grade them. If `git status` shows uncommitted changes to tracked files, say so in the summary.
- The draft PR title and description in `pr_draft.md` (title on the first line, description below it), or whichever files the student's command names.
- The test evidence in `test_evidence.md`.
- The issue named in the command. Gather the thread live (via `gh`, the GitHub API, or the web). A house-chain student reads the house repro pack instead of their own repro.
- The repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`), `docs/CONTRIBUTING.md`, and any stated AI policy.

Read the package the way a reviewer will read the opened PR: the package is what these files and the diff contain, not other files in the working directory. If a named input is missing, say which one in the summary and grade the checks that depend on it `unclear`.

**Eval mode** grades a practice submission bundle (a frozen PR in `eval/packages/`). The bundle text is the whole world. Use only what it contains, fetch nothing, run no git commands, and read nothing else. Grade every check and apply the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the repo the student's PR must belong to and the house rules of that environment (for example, a classmate's claim, plan, or PR does not block the student's own). Apply those rules when reading evidence. Refuse to grade a PR for an issue outside the scoped repo, and say why. If the `Repo:` line still holds an unfilled placeholder, stop without grading and tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after grading the checks, read `voice-guide.md` and hold the outgoing PR text (the title and the description) against the student's rules. Report each rule the text breaks in the summary, quoting the rule and the line that breaks it. The voice guide never changes a check grade or the verdict, because it is the student's own standard. The verdict changes only if the rubric has a check that reads it. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read `rubric.md` for the checks table and the verdict rule, `references/evidence-guide.md` for where each kind of evidence lives, and `procedure.md` for the operating steps. Execute the procedure exactly as written, in order. Do not skip or improvise steps. When the procedure is silent on something you need, do not invent a step: note the gap in the summary so the student can fix it. If `rubric.md` has no written checks, or `procedure.md` has no written steps (only template comments), refuse. Stop without grading, say which file is empty, and do not make up checks. An empty tool that invents checks produces noise that looks like judgment.

## Verdict and output

The verdict is binary: `accept` means the PR is ready to submit, `reject` means hold. There is no third verdict and no score. Put reservations in check evidence lines, not in the verdict. Before the JSON block you may give a short readable summary: a line per check, plus (in live mode) any voice-guide notes and procedure gaps. End your reply with the fenced JSON block below, with one entry per rubric check, valid, and last, with nothing after it. Do not change the schema.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: read the artifact itself against the plan, the issue, and the stated standards, never the formatting. A terse complete PR can be ready, and a polished confident one can hide drift.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary. The fix belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as written and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. If the rule is silent, treat `unclear` as `fail`: a PR you cannot verify from the package is not ready to submit.