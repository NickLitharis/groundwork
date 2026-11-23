# Sources and Scope

This skill was extracted from practitioner review procedures, not from a book. Its principles are a synthesis of the points those procedures agree on. Each claim below is traceable to a source inspected for this skill. The procedures' loop mechanics, persona definitions, and report templates are not part of this skill.

## Inspected sources

- `ds-review-loop` (author-and-fresh-reviewer loop): inspected the scope step, the reviewer brief (review only, no edits, severity classes blocker, should, nit), the rule that a timeout is not approval, the ledger of findings, the four-round limit, and the rule that disputes go to the user. Source: the skill's `SKILL.md` in the local agent skills directory.
- `ponytail-review` (quality review of one change): inspected the importance order, the rule to read callers and the code a change touches, the expected-load judgment, the finding categories (bug, risk, scale, missing test, speed, lean), the requirement for a concrete case, the handling of `shortcut:` markers, and the plain-English output standard. Source: the skill's `SKILL.md` in the local agent skills directory.
- `ponytail-audit` (whole-repository audit): inspected the same importance order and categories, the instruction to grep the whole tree before calling code unused, the rule to say which parts were not read, and the split-by-job rule. Source: the skill's `SKILL.md` in the local agent skills directory.
- `egm-review` (Elephant and Goldfish review protocol): inspected the fresh-context reviewer requirement, the stress-testing default, the rule against sycophantic language, and the artifact-first delivery of long reports. Source: the plugin skill file `skills/egm-review/SKILL.md` in the OMP plugin cache. License: Apache-2.0. This skill does not copy its text.

## Book-derived principles

None. No book was inspected for this skill. The suite's other skills cite books; this one does not.

## Limits and dated claims

- The four procedures were written by different people for different tools, and none has been evaluated against the others. Agreement among them shows that the practices are common, not that they are effective.
- The expected-load and severity rules are judgment-based. The procedures give no measured thresholds.
- Review independence depends on the harness. A reviewer in the same context is not independent; the procedure for `egm-review` says so explicitly.

## Modern application

- The rule to read callers and the code a change touches applies to any language.
- The round limit and rule against approval-by-timeout apply to automated review loops as well as human review.
