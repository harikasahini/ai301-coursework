# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[Issue-72](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72)

**Verdict output**

```
 All three are in scope. Repo facts re-verified against today (2026-09-19); #70 and #72 are unchanged.

  Repo-level evidence (shared)
  - maintainer-active pass — COLLABORATOR Aburke225 pushed on 2026-09-16 (3 days ago) and commented on #52/#43 the same day.
  - maintainer-responsive (preferred) pass — #52 and #43, opened 2026-09-10, drew COLLABORATOR replies on 2026-09-16, ~6 days.
  - repo-not-abandoned pass — archived: false; no releases ever, but last push 2026-09-16 satisfies the ≤90-day branch.
  - ai-workflow-allowed pass — docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI-contribution clause; no AI policy file.
  - low-attempt-history (preferred) pass for all — repo still has zero PRs, open or closed.

  ---

  Accepted, in fit order

  1. #72 — verify_password raises UnknownHashError on malformed stored hashes ← top pick
  - scope-bounded pass — one fix in core/security.py so verification fails closed; acceptance pinned by the existing @pytest.mark.xfail (manifest H-05); 1–2 hours.
  - unclaimed pass — no assignees, zero comments, timeline is four 2026-09-10 label events.
  - good-first-issue-label (preferred) pass — good first issue, plus api, tier-1.
  - Fit: your profile almost verbatim — auth logic, fail-closed security behavior, validation of untrusted stored input. Only candidate here with a good first issue label and a test that defines "done".

  "verdict": "accept"
  }
]

✻ Crunched for 1m 8s · done 12:38 AM

❯ issue-select: grade these candidate first issues: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/70 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/14

"done".

2. #14 — Implement an offline eval runner across a benchmark portfolio set
- scope-bounded pass — one deliverable with the contract already pinned by existing scaffolding: scripts/run_evals.py carries a four-step TODO, EvalSuite.run() already returns relevance_score/faithfulness_score/overall_score, and .github/workflows/eval.yml runs the script with LLM_PROVIDER: mock and reads eval_results.json. Not an index, no disputed design.
- unclaimed pass — no assignees, zero comments, no linked PRs. The one cross-reference is closed issue #43, whose maintainer comment says the shared profile fixtures already landed and "#5, #13 and #14 build on those" — a dependency that's already satisfied, not a claim.
- good-first-issue-label (preferred) fail — labels are enhancement, devops, rag, tests, tier-3.
- Fit: second on fit because it's harness/pipeline orchestration — load fixtures, drive a pipeline against a mock provider, emit a JSON artifact CI consumes — which is closer to your event-driven-pipeline background than parser test plumbing is. Be clear-eyed about the cost: at 7–10 hours and tier-3 it's the largest of the three, it's greenfield with no covering test, and eval.yml runs on any PR touching rag/**, so your work is immediately CI-visible. It passes the rubric as written; if you want an effort ceiling or a covering-test requirement to bite, that belongs in rubric.md.

3. #70 — README parser test fixture is indented, so it contains no headings
- scope-bounded pass — de-indent sample_readme_text in tests/conftest.py, remove xfail H-03; 2–4 hours.
- unclaimed pass — no assignees, zero comments; the 2026-09-16 renamed event is the maintainer.
- good-first-issue-label (preferred) fail — labels are bug, ingestion, tier-2.
- Fit: last, because it's test-fixture whitespace in the ingestion parser — neither API correctness nor service logic. It is the lowest-risk pick though: smallest diff, and the xfail marker tells you exactly when you're done. #71 is the near-identical sibling bug, so expect classmates.

No rejections. Ranking is by fit only — if you'd rather optimize for a fast, certain first merge, take #70 over #14 as the second choice.

  2. #14 — Implement an offline eval runner across a benchmark portfolio set
  - scope-bounded pass — one deliverable with the contract already pinned by existing scaffolding: scripts/run_evals.py carries a four-step TODO, EvalSuite.run() already returns relevance_score/faithfulness_score/overall_score, and .github/workflows/eval.yml runs the script with LLM_PROVIDER: mock and reads eval_results.json. Not an index, no disputed design.
  - unclaimed pass — no assignees, zero comments, no linked PRs. The one cross-reference is closed issue #43, whose maintainer comment says the shared profile fixtures already landed and "#5, #13 and #14 build on those" — a dependency that's already satisfied, not a claim.
  - good-first-issue-label (preferred) fail — labels are enhancement, devops, rag, tests, tier-3.
  - Fit: second on fit because it's harness/pipeline orchestration — load fixtures, drive a pipeline against a mock provider, emit a JSON artifact CI consumes — which is closer to your event-driven-pipeline background than parser test plumbing is. Be clear-eyed about the cost: at 7–10 hours and tier-3 it's the largest of the three, it's greenfield with no covering test, and eval.yml runs on any PR touching rag/**, so your work is immediately CI-visible. It passes the rubric as written; if you want an effort ceiling or a covering-test requirement to bite, that belongs in rubric.md.

  3. #70 — README parser test fixture is indented, so it contains no headings
  - scope-bounded pass — de-indent sample_readme_text in tests/conftest.py, remove xfail H-03; 2–4 hours.
  - unclaimed pass — no assignees, zero comments; the 2026-09-16 renamed event is the maintainer.
  - good-first-issue-label (preferred) fail — labels are bug, ingestion, tier-2.
  - Fit: last, because it's test-fixture whitespace in the ingestion parser — neither API correctness nor service logic. It is the lowest-risk pick though: smallest diff, and the xfail marker tells you exactly when you're done. #71 is the near-identical sibling bug, so expect classmates.

  No rejections. Ranking is by fit only — if you'd rather optimize for a fast, certain first merge, take #70 over #14 as the second choice.

```

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
 {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "maintainer-active", "grade": "pass", "evidence": "COLLABORATOR Aburke225 committed 2026-09-16T21:42:18Z and commented on #52 the same day, 3 days before today"},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "#52 and #43 opened 2026-09-10 each drew a COLLABORATOR reply on 2026-09-16, ~6 days"},
      {"name": "repo-not-abandoned", "grade": "pass", "evidence": "archived: false; no releases, but last push 2026-09-16T21:50:20Z is within 90 days"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "One fix in core/security.py so verify_password returns False; covering xfail H-05 to remove; estimated 1-2 hours"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; zero comments; timeline holds only four 2026-09-10 label events; repo has zero PRs"},
      {"name": "ai-workflow-allowed", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template contain no AI-contribution clause; no AI policy file"},
      {"name": "good-first-issue-label", "grade": "pass", "evidence": "Labels include 'good first issue' alongside bug, api, tier-1"},
      {"name": "low-attempt-history", "grade": "pass", "evidence": "GET /pulls?state=all returns 0 PRs repo-wide, so no abandoned attempts"}
    ],
    "verdict": "accept"
  }
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

```
Run 1: 12/20 scored items (below the 18 bar)
Run 2 (final): 20/20 scored items — matches the agreement line in the committed eval-run.txt
```

**Issue analysis**

```
issue-15: my rubric's verdict is reject; the gold label is reject (agree).Gold's note is years of design debate and two abandoned PRs behind a friendly label.
My rubric initially graded this accept, because unclaimed only checks for a current open PR, and the two linked PRs on this issue (zulip/zulip#20840 and #23123) are both closed, so they didn't trip that check.
I fixed this by adding a clause to scope bounded: or it has a history of stalled attempts like multiple closed unmerged PRs against it." After that change, the issue correctly fails scope-bounded and the verdict flips to reject, matching gold.
```

**Check rationale**

```
Describes one deliverable, completable in a single PR, grade whether the desired outcome is clear, not whether every implementation detailis settled.
Still bounded even with no maintainer comment when the issue lists several contributing causes of one problem (fixing themtogether is the one task),
or lists optional/bonus enhancements beyond a minimal correct fix (those can be skipped or deferred without blocking a merge).
Only fails scope if the outcome itself is ambiguous or disputed: it's really an index of separate, independently trackable
issues, the design is unsettled because reasonable people could disagree on what correct behavior should even be, with no maintainer
ruling, a maintainer flagged core internals work, it's a usage question, not a code change, or it has a history of stalled attempts like multiple closed-unmerged PRs.

I wrote it this way because my first two versions of this check either rejected genuinely bounded bugs (a bug with several listed causes or
optional extra suggestions, like issue-19) or failed to catch a genuinely unbounded one (issue-15's years-long unsettled design). The final
version grades whether the *outcome* is clear rather than whether every detail is settled, which separates "reporter brainstormed some optional
ideas" from "nobody has decided what correct behavior should be.
```

**Trade-offs**
```
This check now correctly passes issues like issue-19 (a bug with two listed causes and three optional performance suggestions) and issue-01(a docs task broken into several related file updates)
that earlier versions of the wording incorrectly rejected — I confirmed both with a canary re-run using --only issue-01,issue-19 after each rewording.

What it gives up: an issue with a genuinely clear, single, obvious fix but where a maintainer has also casually mentioned a possible related
enhancement in the body, with no PR history at all, would now pass scope-bounded even without maintainer confirmation the enhancement is
in scope, the check only fails on stalled *PR* history, not on unconfirmed scope creep with a clean history. I accept this: false
accepts of that shape are rare in the 20-issue set I tested against and easy to catch in live-mode read-through before actually claiming an issue.
```

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**
```
1. The issue's fit to your interests and to the time available.
I have 5+ years building backend services (Java/Spring Boot, REST APIs, distributed systems at Capital One and Discover), so a
service-layer authorization/validation bug like #72 is squarely in my existing skill set, and its 1-2 hour tier-1 estimate fits comfortably
around my other coursework and job commitments, , compared to #14's 7-10 hour estimate.

2. What the verdict identified correctly, and what you weighed that the rubric could not.
The verdict correctly identified that #72 has a fully bounded fix (one function in core/security.py) with a pre-existing xfail test
(manifest H-05) that defines "done" without needing any judgment calls from me. It's also the only one of the three candidates carrying an
actual good-first-issue label alongside tier-1. What the rubric couldn't weigh: I found this genuinely more engaging than the
alternatives, #70 is test-fixture whitespace with no real logic involved, and while #14 is closer to my pipeline/orchestration
background, its 7-10 hour scope and complete lack of a covering test made it a much bigger first commitment than I wanted to take on.

3. The anticipated difficulty in claiming it.
Anticipating low difficulty. The fix is localized to a single function, the target behavior is explicit ("should fail closed, not
raise"), and I can verify correctness by running the existing xfail test rather than writing my own validation criteria. The main risk
noted by the tool is that #70 has a near-identical sibling bug (#71), so classmates may cluster there — a reason in #70's favor if I wanted
the safest possible pick, but not a concern for #72 since nothing suggests contention on it.
```
---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
