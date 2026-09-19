# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-active | Last 5 default branch commits (Repo facts) + maintainer first-response sample | At least one commit or comment from an Owner/Member/Collaborator within 90 days of the capture date; a bot merge counts only if it merged a human's PR or if a human (non-bot) account merged the bot's PR. A bot merging another bot's PR does not count. | required |
| maintainer-responsive | Maintainer first-response sample across the 5 most recently updated issues | An Owner/Member/Collaborator has replied to at least one other issue within 1-2 weeks of it being opened | preferred |
| repo-not-abandoned | Latest release + last push to any branch (Repo facts) | Repo is not archived, with either a release in the last 12 months or a push to any branch in the last 90 days. | required |
| scope-bounded | Issue title/body + thread | Describes one deliverable, completable in a single PR, grade whether the desired outcome is clear, not whether every implementation detail is settled. Still bounded even with no maintainer comment when the issue lists several contributing causes of one problem (fixing them together is the one task), or lists optional/bonus enhancements beyond a minimal correct fix (those can be skipped or deferred without blocking a merge). Only fails scope if the outcome itself is ambiguous or disputed: it's really an index of separate, independently trackable issues, the design is unsettled because reasonable people could disagree on what correct behavior should even be, with no maintainer ruling, a maintainer flagged core internals work, it's a usage question, not a code change, or it has a history of stalled attempts like multiple closed-unmerged PRs. | required |
| unclaimed | Assignees + linked PRs + comment thread (Repo facts / Comments) | No current assignee, no open linked PR, no unanswered "I'll take this" style claim from another contributor. If the thread contradicts the Assignees/Development box, trust the thread, read the full comment history, not just the sidebar | required |
| ai-workflow-allowed | CONTRIBUTING.md / AI policy files / templates (contribution policy line) | Not an outright ban on AI-generated contributions. Disclosure or human-review conditions are fine (pass); silence is fine (pass); explicit ban is fail | required |
| good-first-issue-label | Issue labels | Issue is labeled good-first-issue or equivalent | preferred |
| low-attempt-history | Issue history | Issue does not already have multiple abandoned/unmerged PRs against it | preferred |

## Verdict rule

Accept only if every `required` check passes. A `?` (not enough evidence
in the bundle/page to decide) on a required check counts as a fail.
`preferred` checks never change the verdict, they only help you break
ties between multiple accepted issues when you get to live mode.
