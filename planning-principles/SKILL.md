---
name: planning-principles
description: Apply software-engineering fundamentals and Unix philosophy to scope and plan coding work. Use when requirements are ambiguous, a change has consequential dependencies or risks, or the user asks for a scope, implementation plan, feasibility assessment, or work breakdown. Define outcomes, boundaries, acceptance evidence, uncertainty, and verifiable increments. Avoid formal planning for trivial, well-understood edits.
---

# Planning Principles

Define the smallest coherent outcome that satisfies the actual need. Investigate enough to choose a credible approach, resolve consequential uncertainty early, and plan verifiable increments. Preserve the ability to change direction without silently changing the commitment.

## Fundamentals

- **Scope is a commitment.** Define the problem, intended users, required outcomes, inclusions, exclusions, constraints, and observable success. A proposed implementation is not necessarily the underlying requirement.
- **A plan is a reasoned approach, not a prediction of certainty.** Explain dependencies, assumptions, verification, and the next decisions. Separate observed facts from hypotheses and unresolved choices.
- **Feasibility precedes commitment.** Inspect relevant code, consumers, tests, existing capabilities, and operational constraints. Do not invent file paths, APIs, estimates, or acceptance commands from memory.
- **Risk determines investigation and sequencing.** Address unknowns that could invalidate the approach early. A small experiment can be more useful than a detailed speculative plan. Define its question, bounded effort, evidence, and decision before starting.
- **Progress means demonstrated outcomes.** Prefer coherent, end-to-end increments that can be verified. Infrastructure-only steps may be necessary, but identify the outcome they enable and their integration point.
- **Estimates express uncertainty.** Use comparable work and known constraints when estimating. State assumptions and ranges where justified; do not invent precision. Distinguish effort, elapsed time, external lead time, and a requested deadline.
- **Measure outcomes, not activity.** Choose measures that reflect the intended user or system result. Commit counts, tickets closed, lines produced, and other activity counts are not outcomes by themselves; broader productivity cannot be reduced to a single measure.
- **Plans evolve; scope changes are explicit.** Refine near-term work more precisely than distant work. Requirements work may iterate through elicitation, analysis, specification, and validation; do not demand complete certainty before useful feedback. Revise when evidence changes. Do not silently drop requirements, expand the task, or treat sunk effort as justification to continue a failed approach.
- **Planning has a cost.** Scale detail and documentation to uncertainty, impact, reversibility, and coordination needs—not file count. A straightforward local edit may need only a short statement and a check.

## Working loop

1. **Understand the need.** Identify the desired behavior and why it matters. Separate requirements from suggested solutions. Discover what tools and repository evidence can answer; ask the user only about unresolved consequential choices.
2. **Map the boundary.** Identify affected components, public contracts, data, consumers, and external systems. State what is included and excluded, and relevant security, compatibility, performance, resource, or regulatory constraints. Missing safety work is not a legitimate scope reduction.
3. **Define success.** Make acceptance criteria observable. Verification asks whether the implementation meets its specification; validation asks whether it solves the intended problem. Plan evidence for both when they differ.
4. **Resolve blocking uncertainty.** Inspect existing implementations and alternatives. Select the simplest sufficient approach. Test risky assumptions before committing to work that depends on them; defer reversible details that need no decision yet.
5. **Sequence the work.** Choose the user or program interface for the actual workflow before splitting tasks, then break the outcome into cohesive changes ordered by actual dependencies and risk. For each step identify the intended result, affected component, prerequisites, and a concrete check. Parallelize only genuinely independent work with clear ownership and agreed interfaces.
6. **Include completion work.** Account for integration, tests, documentation, affected consumers, deployment, data migration, cleanup, and recovery where relevant. A code patch is not the whole delivery when these are necessary.
7. **Critique once where useful.** Look for missing requirements, unsupported assumptions, omitted failure paths, and a simpler approach. Do not turn repeated planning into a substitute for implementation. Stop planning when remaining uncertainty is acceptable for the next safe action.
8. **Execute only within authorization.** A request for a plan alone does not authorize implementation. Once execution is requested, work through the plan, collect evidence, and revise affected steps when observations invalidate assumptions. Seek a decision before a material change to the agreed outcome or risk.

### Evidence, project practices, and reuse

- For a bug, bound investigation before promising a fix: gather relevant observations, state competing hypotheses, and define what evidence would confirm, reject, or change the approach. Plan how diagnosis and recovery will be accepted, not only the happy path.
- Discover the repository’s actual commands, prerequisites, and CI checks before scheduling work. Reuse them; when meaningful verification is unavailable, say why and choose proportionate evidence rather than inventing tools or silently skipping risk.
- Identify generated artifacts and their source before planning edits; generation rules are owned by [minilanguage-generation-principles](../minilanguage-generation-principles/SKILL.md).
- Include documentation work only when it materially helps the affected audience; organization rules are owned by [documentation-principles](../documentation-principles/SKILL.md).
- Before adopting a reuse candidate, assess fit, documentation, license, support, integration, updates, and exit cost. Compare only credible options; do not turn planning into speculative procurement or default package installation.

For examples and decision checks, see [Planning foundations](references/chapter-foundations.md) when relevant.


## Complexity and performance decisions

Simplify the design, not the commitment. Changing an agreed outcome or a chosen feature is a scope decision, not a simplification, so record it as one. How to reduce implementation complexity is owned by [engineering-principles](../engineering-principles/SKILL.md); how to measure and stop optimization is owned by [performance-principles](../performance-principles/SKILL.md).

## Practical tradeoffs

- **Small scope versus incomplete delivery:** a CSV export may exclude XML and plugins, but still needs correct escaping, authorization, and a usable delivery path.
- **Early feedback versus hard dependencies:** prefer an end-to-end slice, but do a feasibility experiment first if a required external API may not support the operation. Document what would make you abandon or change the approach.
- **Flexibility versus compatibility:** a private function can change with its callers; a persisted format or independently deployed consumer may require versioning or staged migration. Plan for the actual boundary.
- **Fixed deadline versus uncertain scope:** make tradeoffs explicit. Do not promise all outcomes by removing verification or concealing uncertainty. Scope reduction requires agreement.

## Output

For substantial work, provide a concise scope and plan containing:

- Goal and observable acceptance criteria.
- Included behavior, explicit exclusions, and constraints.
- Evidence gathered, important assumptions, and open decisions.
- Chosen approach and the consequential tradeoff, if any.
- Ordered steps with dependencies and verification.
- Relevant delivery, migration, recovery, and completion conditions.

Omit irrelevant sections for small work. Persist the plan only when requested or useful for coordination and continuity; do not require a PLAN.md for every task. Avoid principle scores and boilerplate reports.

Keep code-design guidance in the companion engineering-principles skill; this skill owns deciding the work and its sequence, not a second implementation rulebook.
Use engineering-principles for implementation design; route focused diagnosis, testing, safe evolution, reliability, or security concerns to debugging-principles, testing-principles, evolution-principles, reliability-principles, or security-principles as needed. Planning decides what work and evidence are needed; it does not replace those specialist workflows.

