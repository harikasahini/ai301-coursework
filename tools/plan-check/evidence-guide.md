# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- Where it lives: In an eval package, the Candidate plan's stated cause (usually under a "Diagnosis" or "Cause" heading), read against the specific behavior, traceback, or timing shown in the Repro evidence section. Live, the plan draft's stated cause, read against the student's own posted repro comment on the issue.
- What good looks like: The stated cause is something the repro evidence actually demonstrates, not merely something the issue or thread speculated about. If the repro evidence shows a behavior that contradicts the stated cause (for example, a timing test that rules out one mechanism), the diagnosis must account for that, not ignore it.

## Scope

- Where it lives: In an eval package, the Candidate plan's stated scope and file list (usually under "Scope" or "Changes"), read against the diagnosis above it. Live, the same, in the plan draft.
- What good looks like: The named files and the stated "won't touch" boundary are reachable from the diagnosis, not merely present. A scope that is tightly bounded but reaches the wrong file, or a scope that quietly grows to cover a second problem, both fail, even though one looks minimal and the other looks thorough.

## Executability

- Where it lives: In an eval package, the Candidate plan's approach or "Changes" section. Live, the plan draft's approach section.
- What good looks like: A stranger could start making the change from what's written: specific functions, files, or call sites are named, not just a general description of the problem area.

## Test plan

- Where it lives: In an eval package, the Candidate plan's test plan (however labeled), read against the Repro evidence section's own steps. Live, the plan draft's test plan, read against the student's posted repro comment.
- What good looks like: The test plan re-runs or clearly adapts the repro evidence's own steps, and states a concrete, observable change expected between before and after (what output, what timing, what rendered state). Whether the plan also adds an automated test is not what decides this: a manual re-run of the repro steps that states a clear observable outcome is sufficient.

## Honesty

- Where it lives: The plan's risks or unknowns section (if any), read against the assumptions its diagnosis and approach actually rest on. Eval and live work the same way.
- What good looks like: An assumption the diagnosis depends on (for example, that a fix in one call site covers all code paths that hit the bug) is named as a risk if it hasn't been verified, not folded silently into the plan as settled fact.

## Comms

- Where it lives: In an eval package, the Candidate plan comment, read against the Thread highlights and the Repo facts block's stated conventions. Live, the plan comment draft, read against the issue thread and the repo's CONTRIBUTING.md or equivalent.
- What good looks like: The comment doesn't ignore an open question, a competing theory, or a constraint raised in the thread (for example, a maintainer's note about limited review time), and it follows what the repo's conventions ask of a plan or approach comment. If the repo's policy requires disclosing AI assistance, the comment discloses it.
