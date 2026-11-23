---
name: engineering-principles
description: Use when implementing, fixing, refactoring, or reviewing code, or designing a module or API. Covers simplicity, contracts, complexity, abstraction, dependencies, and verified changes. Not prose-only edits.
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

Diagnose failures with [debugging-principles](../debugging-principles/SKILL.md), not by guesswork in the code.

Use the repository's existing build, test, run, and generation entry points. Read their documented prerequisites and invoke the same commands humans and CI use; do not add a second toolchain or require Make where the repository has another suitable interface. A test command with no matching tests is no proof.

Update affected documentation as part of the change, following [documentation-principles](../documentation-principles/SKILL.md).

## Design principles

### Correctness starts with contracts

Define what must remain true before choosing a pattern. Make invalid states difficult to represent using suitable types, constructors, and explicit state transitions. Keep ownership of mutable state and resource lifetimes clear.

Validate untrusted input at boundaries. Do not remove checks merely because they look defensive: establish whether the condition is impossible, already guaranteed, or still a real failure mode. Preserve useful error context without leaking secrets. Never turn failure into an invented successful result.

### Simplicity: KISS and YAGNI

KISS means minimize the complexity a maintainer must understand, not merely the line count. YAGNI means implement current requirements rather than speculative future features. Neither excuses missing error handling, unsafe storage, or an unmaintainable shortcut.

Avoid plugins, generic frameworks, configuration layers, or extension points without a present need. A simple design can still have clear boundaries that make later change inexpensive.

### Complexity across the system

Distinguish essential complexity (required by the problem), optional complexity (a capability with a cost), and accidental complexity (avoidable difficulty in implementing specified behavior). Use these as reasoning categories, not a feature quota. Apply them across implementation, interface, integration, and users’ effort and error risk: lowering cost in one place can shift it elsewhere. Remove accidental complexity; keep optional capability when its user value justifies its full-life cost. Under a deadline, compare delivery value now with end-to-end effort, support, and maintenance; fewer lines or features alone do not establish lower total cost. For examples, see [Complexity](references/complexity.md).

### Module boundaries

Module boundaries, depth, and information hiding are owned by [modularity-principles](../modularity-principles/SKILL.md). Apply that skill when deciding where a boundary belongs. This skill adds one constraint: an interface should be no more general than its current callers justify, because guessed future needs burden present callers.

### Abstraction and DRY

DRY means one authoritative representation of a piece of knowledge, not eliminating every similar-looking sequence. Share logic when callers express the same rule and should evolve together. Keep superficially similar code separate when it belongs to different concepts or lifecycles.

Generated files are owned by [minilanguage-generation-principles](../minilanguage-generation-principles/SKILL.md): edit the source and regenerate, never the output.

Before extracting, identify the shared contract, the expected reasons for change, and the complexity the abstraction removes. Do not use a numerical repetition threshold as proof. A little duplication can cost less than the wrong coupling.

### SOLID as diagnostic questions

Use these questions where the design benefits; do not impose an object-oriented architecture on procedural or functional code.

- **Single responsibility:** does this unit mix independently changing concerns?
- **Open/closed:** is there a demonstrated axis of variation worth isolating, rather than a hypothetical extension framework?
- **Liskov substitution:** can an implementation replace another without surprising callers through stronger preconditions, weaker guarantees, or incompatible failures?
- **Interface segregation:** do consumers depend only on capabilities they use?
- **Dependency inversion:** should a stable policy depend on a narrow contract instead of volatile I/O details? A function or parameter can provide that seam; a class hierarchy is not required.

Prefer composition over inheritance when inheritance does not model a genuine substitutable relationship. Use language-idiomatic mechanisms rather than pattern names as a goal.

### Readability

Choose names that expose domain meaning, units, and ownership. Keep control flow and side effects easy to follow. Use comments for rationale, constraints, and non-obvious guarantees, not to narrate obvious statements.

Follow repository conventions unless they cause a concrete problem. Function size, parameter count, and nesting depth are warning signs, not universal numeric limits. Extra indirection is not automatically cleaner code. Comments can preserve rationale, constraints, and an abstraction that code alone does not explain; judge their value in context rather than removing them or splitting cohesive logic to meet a length or comment-count rule.

### Dependencies

Reuse a maintained, appropriate library for difficult established capabilities, especially cryptography and protocol handling. Evaluate fit, security, license, compatibility, operational cost, and dependency weight. Do not add a dependency for a trivial operation already served by the language or repository.

Performance measurement and optimization are owned by [performance-principles](../performance-principles/SKILL.md). This skill keeps one constraint: a stated latency or memory requirement is a contract, and simplicity does not justify breaking it.

## Other skills' ground

- Module boundaries and interface depth: [modularity-principles](../modularity-principles/SKILL.md).
- Unix design rules, composition, and CLI and config conventions: [unix-philosophy](../unix-philosophy-principles/SKILL.md), [composition](../composition-principles/SKILL.md), [interface](../interface-principles/SKILL.md), [configuration](../configuration-principles/SKILL.md).
- Visibility and failure reporting: [transparency](../transparency-principles/SKILL.md).
- Behavior-preserving change and compatibility: [evolution](../evolution-principles/SKILL.md). Test design: [testing](../testing-principles/SKILL.md).

Read those skills when their concern is the deciding factor. Choose the interface style by its human and machine consumers, not by tradition, and follow the simplest style that meets the contract.

## Final decision check

Before declaring completion, ask:

- Does the implementation satisfy the actual contract, including relevant failures?
- Is each abstraction, dependency, and changed file justified by this task?
- Can a maintainer locate the rule, its state owner, and the evidence protecting it?
- Did I preserve existing behavior or make the intended change explicit across affected consumers?
- What did I actually verify, and what remains unverified?

Use this check privately; do not emit a boilerplate report or principle score for every edit.

