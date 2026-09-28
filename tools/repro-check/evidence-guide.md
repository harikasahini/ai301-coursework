# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

# Evidence guide: where proof lives in a reproduction package

## Environment

- Where it lives: In an eval package, the Candidate repro report's text (it has no separate environment section, so look for OS, versions, or a commit in what it says), read against the target named in the Issue section.
- What good looks like: The versions named match what the issue targets, or the difference is called out. A stranger could rebuild the same setup from what is written without guessing.

## Steps

- Where it lives: In an eval package, the Candidate repro report's text.
- What good looks like: The steps run from a clean starting state to the trigger with exact commands, inputs, and files, not "set up the project". A stranger can follow them without asking a question.

## Behavior shown

- Where it lives: In an eval package, quoted output, logs, or screenshots in the Candidate repro report, read against the behavior in the Issue section. A description in words with no quoted output is a statement, not an artifact.
- What good looks like: The artifact shows the same behavior the issue describes (same error, same failing input), not a nearby failure. The output shown is what the steps would actually produce.

## Honesty

- Where it lives: In an eval package, the outcome the Candidate repro report states, compared with what it quotes or shows.
- What good looks like: Every claim has an artifact behind it. A report that says it could not reproduce and shows what was tried is honest and ready. A report that says it confirmed the bug without matching output, or with output showing something else, claims more than it shows.

## Comms

- Where it lives: In an eval package, the Candidate claim comment read against the Issue section, and both candidates read against the Repo facts lines on the bug-report template and the contribution policy.
- What good looks like: The claim refers to details of this issue and says what the author will do next, not boilerplate that would fit any issue. The comments supply what the repo's template asks for. If the repo's policy requires disclosing AI assistance, the comments disclose it; a policy that says nothing about AI requires nothing.
