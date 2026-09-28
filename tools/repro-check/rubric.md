# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The repro report's environment record, read against the version or setup the issue targets | Names enough (OS, runtime and tool versions, repo commit or release) for a stranger to rebuild the setup, and the versions match what the issue targets or the difference is called out | required |
| steps-followable | The repro report's steps, from starting state to trigger | Every action needed to reach the trigger is concrete enough to run without guessing (commands, inputs, files); a missing prerequisite or a step like "set up the project" fails | required |
| behavior-matches-issue | Output excerpts, logs, or screenshots in the repro report, read against the behavior in the issue context | The artifact shows the same behavior the issue describes (same error, same failing input) and could result from the steps given; an adjacent or different failure fails | required |
| outcome-honest | The report's stated outcome, read against its artifacts | The stated outcome (reproduced or not) is backed by the artifacts shown; an evidenced cannot-reproduce passes; a claimed reproduction the artifacts do not show fails | required |
| claim-specific | The claim comment, read against the issue context | Refers to details that belong to this issue (the function, error, or file it names) and says what the author will do next; boilerplate that would fit any issue fails | required |
| conventions-followed | Both comments, read against the repo-facts block (stated bug-report template asks and contribution policy) | The comments give what's needed to evaluate this reproduction: environment or version info sufficient to place the bug, and any template field materially relevant to it (not every field the template lists, if it doesn't bear on this bug). If the repo's stated policy requires disclosing AI assistance, the comments disclose it; a policy silent on AI use requires nothing. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept if every required check passes. Preferred checks never change the
verdict. Unclear counts as fail.