---
name: engineering-principles
description: Apply fundamental software engineering principles and Unix philosophy when implementing features, fixing bugs, designing modules or APIs, refactoring, or reviewing code. Use especially for decisions about simplicity, abstraction, duplication, coupling, contracts, testing, dependencies, performance, CLI tools, and composability. Turn principles into concrete tradeoffs and verified changes, not ritual checklists. Not for prose-only edits or unrelated non-coding tasks.
---

# Engineering Principles

Build the smallest correct solution that remains understandable and safe to change. Treat principles as tools for reasoning, not laws that outrank requirements, repository conventions, or evidence.

## Working loop

1. **Establish the contract.** Read the relevant code, callers, tests, and repository instructions. Identify required behavior, inputs, outputs, invariants, failure modes, and compatibility constraints. Distinguish observed facts from assumptions. Ask only when an unresolved requirement materially changes the solution.
2. **Choose a proportionate design.** Reuse local patterns and existing capabilities. Prefer a direct implementation; add structure when it contains real complexity or protects an actual boundary. Consider security, data integrity, and resource limits where the change touches them.
3. **Change one concern at a time.** Keep the diff cohesive. Preserve unrelated work. Separate behavior-preserving refactoring from intentional behavior changes so each is reviewable. Fix the cause, not just the observed symptom.
4. **Verify the promised behavior.** Use the narrowest meaningful test or executable scenario, including relevant failure paths. Inspect what actually ran; an empty test selection proves nothing. Passing tests are evidence for the assertions and paths they exercise, not proof of all correctness or compatibility.
5. **Finish the change.** Update affected callers, contracts, and documentation. Remove code made obsolete by this change. Report the result, verification, and any remaining limitation briefly; explain a principle only when it materially influenced a decision.

Scale this loop to risk: a local rename needs little ceremony; a shared API or persisted-data change needs consumer and migration evidence. Do not manufacture design documents or a specialist chain for routine edits.

## Debugging and repository workflow

Treat a user-reported failure as a reproduction; do not ask them to repeat it merely to confirm it. Separate observed behavior from hypotheses, then gather evidence that distinguishes likely causes. Use a focused reproduction, targeted inspection, or debugger rather than changing code by guesswork. Fix the cause, preserve useful diagnostics without exposing secrets, and never suppress an error to make the path appear successful. Add missing regression coverage and verify relevant recovery behavior when failure can leave partial state.

Use the repository's existing build, test, run, and generation entry points. Read their documented prerequisites and invoke the same commands humans and CI use; do not add a second toolchain or require Make where the repository has another suitable interface. A test command with no matching tests is no proof.

Maintain useful contributor documentation: preserve the why, invariants, and key flows that code alone does not explain; update affected docs, choosing user reference, tutorial, or troubleshooting material for the audience. Avoid broad doc rewrites unrelated to the change.

## Design principles

### Correctness starts with contracts

Define what must remain true before choosing a pattern. Make invalid states difficult to represent using suitable types, constructors, and explicit state transitions. Keep ownership of mutable state and resource lifetimes clear.

Validate untrusted input at boundaries. Do not remove checks merely because they look defensive: establish whether the condition is impossible, already guaranteed, or still a real failure mode. Preserve useful error context without leaking secrets. Never turn failure into an invented successful result.

### Simplicity: KISS and YAGNI

KISS means minimize the complexity a maintainer must understand, not merely the line count. YAGNI means implement current requirements rather than speculative future features. Neither excuses missing error handling, unsafe storage, or an unmaintainable shortcut.

Avoid plugins, generic frameworks, configuration layers, or extension points without a present need. A simple design can still have clear boundaries that make later change inexpensive.

### Complexity across the system

Distinguish essential complexity (required by the problem), optional complexity (a capability with a cost), and accidental complexity (avoidable difficulty in implementing specified behavior). Use these as reasoning categories, not a feature quota. Apply them across implementation, interface, integration, and users’ effort and error risk: lowering cost in one place can shift it elsewhere. Remove accidental complexity; keep optional capability when its user value justifies its full-life cost. Under a deadline, compare delivery value now with end-to-end effort, support, and maintenance; fewer lines or features alone do not establish lower total cost. For examples, see [Complexity, Interfaces, and Performance](references/complexity-performance.md).

### Cohesion, coupling, and information hiding

Group code that changes for the same reason; separate concerns that change independently. Hide volatile implementation choices behind a small, coherent interface. Prefer a deep module that does useful work over a chain of pass-through wrappers.

An interface may be somewhat general-purpose when that lets a shared mechanism serve identifiable callers without embedding one caller's policy. Keep it no more general than current uses justify: guessed future needs can burden present callers. Choose a specialized interface when its contract genuinely is specific.

Single responsibility concerns a coherent reason to change, not one method per class. Low coupling means consumers need little knowledge of internals, not that every call requires an interface. Keep dependency directions explicit and avoid cycles where practical.

### Abstraction and DRY

DRY means one authoritative representation of a piece of knowledge, not eliminating every similar-looking sequence. Share logic when callers express the same rule and should evolve together. Keep superficially similar code separate when it belongs to different concepts or lifecycles.

When knowledge also appears in generated files, identify its authoritative source and generator. Protect unrelated edits before regeneration; resolve overlapping ownership rather than overwrite user work. Update the source, run the existing generator, and inspect the derived diff. Do not hand-edit generated output as the durable fix or add generation machinery for trivial work.

Before extracting, identify the shared contract, the expected reasons for change, and the complexity the abstraction removes. Do not use a numerical repetition threshold as proof. A little duplication can cost less than the wrong coupling.

### SOLID as diagnostic questions

Use these questions where the design benefits; do not impose an object-oriented architecture on procedural or functional code.

- **Single responsibility:** does this unit mix independently changing concerns?
- **Open/closed:** is there a demonstrated axis of variation worth isolating, rather than a hypothetical extension framework?
- **Liskov substitution:** can an implementation replace another without surprising callers through stronger preconditions, weaker guarantees, or incompatible failures?
- **Interface segregation:** do consumers depend only on capabilities they use?
- **Dependency inversion:** should a stable policy depend on a narrow contract instead of volatile I/O details? A function or parameter can provide that seam; a class hierarchy is not required.

Prefer composition over inheritance when inheritance does not model a genuine substitutable relationship. Use language-idiomatic mechanisms rather than pattern names as a goal.

### Readability and least surprise

Choose names that expose domain meaning, units, and ownership. Keep control flow and side effects easy to follow. Use comments for rationale, constraints, and non-obvious guarantees, not to narrate obvious statements.

Follow repository conventions unless they cause a concrete problem. Function size, parameter count, and nesting depth are warning signs, not universal numeric limits. Extra indirection is not automatically cleaner code. Comments can preserve rationale, constraints, and an abstraction that code alone does not explain; judge their value in context rather than removing them or splitting cohesive logic to meet a length or comment-count rule.

### Dependencies and performance

Reuse a maintained, appropriate library for difficult established capabilities, especially cryptography and protocol handling. Evaluate fit, security, license, compatibility, operational cost, and dependency weight. Do not add a dependency for a trivial operation already served by the language or repository.

Choose sensible data structures and algorithms for expected input sizes. Avoid obvious redundant work and wasteful allocation or copying. Measure suspected bottlenecks before complex optimization; benchmark representative workloads and protect correctness. Name the workload, metric, baseline, target, and stop criterion; use measures tied to actual user or system outcomes, not activity counts. Stop once the contract is met or further gain is not worth added complexity and maintenance. Decide whether the contract values latency, throughput, or resource use: batching can improve throughput while worsening response time. Do not trade away a stated latency or memory requirement for stylistic simplicity. For examples, see [Complexity, Interfaces, and Performance](references/complexity-performance.md).

## Unix philosophy in practice

Write cohesive components that do one job well and compose through explicit contracts. This does not require one process per function, microservices, text-only storage, or statelessness everywhere. Internal libraries with clear APIs can be equally composable.

- **Separate mechanism from policy.** Keep reusable computation independent of presentation, environment, and changing business choices where that separation reduces coupling.
- **Design for composition.** Avoid hidden global state and unnecessary hardcoded paths. Make dependencies and effects explicit; let callers choose destinations where appropriate.
- **Prefer inspectable representations.** Use simple data structures and documented formats. Text is valuable for interoperable tools; binary formats are valid when fidelity, volume, or performance requires them.
- **Keep ordinary operation quiet, failures visible.** Silence means no irrelevant chatter, not missing result data or suppressed diagnostics.
- **Reuse tools.** Prefer existing reliable capabilities over rebuilding them. Keep automation noninteractive when it is intended for scripts.

Choose interface style by its human and machine consumers, not tradition. A function or library API, stable CLI, or filter can suit machine callers and repeatable work; human tasks may need discoverability, feedback, or direct interaction. If both are real consumers, separate domain logic from optional wrappers so they share behavior without making a GUI mandatory. Follow the simplest style that meets the contract. See [Unix interfaces](references/unix-interfaces.md) and [Complexity, Interfaces, and Performance](references/complexity-performance.md) for practical tradeoffs.
For CLI, pipeline, and configuration design, read [Unix interfaces](references/unix-interfaces.md). When complexity, interface style, or performance tradeoffs materially shape the decision, read [Complexity, Interfaces, and Performance](references/complexity-performance.md). For competing principles and examples, read [Tradeoffs](references/tradeoffs.md). These references are conditional; none is mandatory for an unrelated local edit.
For practical debugging, project commands, generated artifacts, maintainer documentation, and dependency evaluation examples, read [Debugging and Maintenance](references/debugging-maintenance.md).

## Safe evolution and verification

A refactor preserves observable behavior, including outputs, errors, side effects, and contracts consumers rely on. Do not silently fix quirks during a refactor. An intentional contract change instead updates affected tests and consumers explicitly; tests of superseded requirements are not permanent constraints.

Protect public boundaries with behavior-focused tests. Reuse adequate coverage; add regression or characterization tests when an important path is unprotected. Prefer real implementations or focused fakes where practical, but use doubles to isolate genuinely costly, nondeterministic, or unsafe boundaries. Avoid assertions about private method calls or exact source wording unless those are themselves the contract.

Check meaningful edge cases: malformed inputs, empty data, resource failure, and concurrency or partial writes when relevant. Do not prescribe an arbitrary coverage percentage or a full suite for every edit.

Preserve public compatibility unless changing it is in scope. For durable contracts and persisted data, examine consumers, deployment order, migration, and recovery. Use expand/contract or another staged approach when old and new versions must coexist; a coordinated atomic change may suffice otherwise. Do not drop recovery paths or install compatibility shims without an actual requirement.

## Final decision check

Before declaring completion, ask:

- Does the implementation satisfy the actual contract, including relevant failures?
- Is each abstraction, dependency, and changed file justified by this task?
- Can a maintainer locate the rule, its state owner, and the evidence protecting it?
- Did I preserve existing behavior or make the intended change explicit across affected consumers?
- What did I actually verify, and what remains unverified?

Use this check privately; do not emit a boilerplate report or principle score for every edit.

