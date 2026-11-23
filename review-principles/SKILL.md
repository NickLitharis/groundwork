---
name: review-principles
description: Use when judging a change, a repository, or a design before it ships: deciding what a review must check, whether a finding is real, how severe it is, how a reviewer independent of the author should work, and when a review is finished. Not the mechanics of a particular review tool, loop, or report template, and not test design (testing-principles owns that).
---

# Review to find what would break, and say why

A review is useful only when its findings are real, specific, and ranked by consequence. Lead with what would fail for a user or the system, give each finding a case that shows it, and propose the smallest fix. A review that lists style preferences or vague worries costs the author time and teaches them nothing.

## Order the concerns

Check in this order of importance: correct, safe, holds under the expected load, tested, fast enough, lean. Lean still matters, because every extra line must be read, tested, and maintained later. Name the scope the review covers and what it leaves out.

## Require a concrete case for every finding

A finding states an input or situation and the wrong result it produces: "when the list is empty, the total is returned as zero instead of an error." If you cannot state the case, do not report the finding. Before you claim code is unused, search the whole tree, including tests, configuration, and dynamic references. Before you claim a caller is broken, find the caller.

## Read beyond the diff

Before you judge a change, read its callers and the tests that cover the changed code. A broken caller is a finding only with the caller's file and line. If you did not read a caller, list it as unchecked in the verdict, so the author knows where the review stopped. A fix applied in one caller while a shared function stays broken is a finding. Proving that a change is safe outside its diff is covered by [evolution-principles](../evolution-principles/SKILL.md).

## Judge scale against the stated load

Code that is correct for one user can fail for many: check-then-write races, work repeated by every process, lists that only grow, a query per item. Find the expected load in the project's documentation or configuration, judge against it, and say which load you assumed. A shortcut the code marks with its limit is a decision, not a finding, unless the expected load already exceeds that limit.

## Propose the smallest fix

Prefer a fix that deletes code, narrows it, or reuses an existing helper over one that adds a layer, a dependency, or configuration. Split code only by job, never by line count, and never into helpers that exist only to shorten a function. Fewer lines can still hide a defect; a fix must be checked against the case that motivated it.

## Keep the reviewer independent

The reviewer should not share the author's context, or the review confirms the author's assumptions. A reviewer reads and reports; it does not edit the code under review. Keep one reviewer working at a time, so findings do not collide.

Do not treat a timeout, an error, or an empty reply as approval. Do not agree with a finding just to end a review. When author and reviewer disagree, decide each point on evidence such as a test result or the code at a specific line. A dispute that evidence does not settle belongs to the person who owns the decision, reported with both positions.

## Stop at a defined point

A review ends when no finding about correctness, safety, or expected-load behavior is open, or when a further round would produce only nits. Set a round limit in advance so a review cannot run indefinitely. A review that hits its limit with open disputes is reported as unresolved, not as approved.

## Rank and report

Group findings by consequence, not by location: a fault that breaks users or loses data outranks one that makes code harder to read. Number the findings so they can be referred to in discussion. Each finding should say what the code does, what goes wrong, the fix, and what happens if the fix is skipped. Close with a verdict and the parts that were not checked.

Write in plain sentences. Explain a technical term the first time it appears. Leave out praise without substance and words such as "consider" or "might be worth" that hide whether the problem is real.

## Watch for these failure modes

- Findings without a case, or cases the reviewer did not verify.
- A review that reads only the diff and misses a broken caller.
- Style preferences reported as defects.
- Approval given because the author pushed back, not because the evidence changed.
- A reviewer that edits the code while reviewing it.
- Unbounded loops that end only when someone gives up.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [testing](../testing-principles/SKILL.md) for whether tests protect a behavior, [debugging](../debugging-principles/SKILL.md) for finding a cause, [security](../security-principles/SKILL.md) for trust boundaries, [engineering](../engineering-principles/SKILL.md) for the design a review is judging.
