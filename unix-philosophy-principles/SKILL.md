---
name: unix-philosophy-principles
description: Use when deciding a program's scope, whether a feature belongs in a tool or library, how a new component should compose with existing ones, or when a design is growing large or clever. Applies the Unix design rules as tradeoff tests. Not a mandate for microservices, text-only interfaces, or any particular toolchain.
---

# Design with the Unix rules as tests

The Unix rules are a compact set of design heuristics developed around small programs that cooperate through simple interfaces. Use them to test a design, not to prove one. When a rule conflicts with the actual requirement, the requirement wins, and the conflict should be stated.

## Test the design against the rules

Name the job the component must do in one sentence. If the sentence needs "and" several times, the component may be carrying more than one responsibility; consider separating them (Rule of Modularity, Rule of Simplicity).

Keep policy separate from mechanism, and interfaces separate from engines (Rule of Separation). A component that decides what should happen is easier to change than one that also implements how it happens.

Prefer parts that can be connected to other parts (Rule of Composition). Ask whether the output could feed another tool or whether a caller could use the component without the rest of the system.

Choose the clearer design when the two conflict. "Clarity is better than cleverness" (Rule of Clarity). A clever solution that only its author can read is a maintenance cost that will be paid later.

Write a big component only when a demonstration shows that nothing smaller will do (Rule of Parsimony). Size applies to code volume and internal complexity alike.

Distrust any claim of "one true way" when the problem has several reasonable solutions (Rule of Diversity). Compare alternatives on the concrete constraints before choosing.

## Rules owned by other skills

This skill only maps the rules to their owners. Optimization (Rule of Optimization) belongs to [performance-principles](../performance-principles/SKILL.md). Extensibility without speculative features belongs to [engineering-principles](../engineering-principles/SKILL.md). Modularity, composition, and transparency belong to their own skills, linked below.

## Watch for these failure modes

- Growing one program to cover adjacent jobs instead of connecting two small ones.
- Adding a clever abstraction where a plain function or data structure would do.
- Keeping a design because effort was already spent on it. The book describes this as overinvestment in failed approaches.
- Treating the rules as a reason to split systems into many services. The rules govern interfaces and responsibilities, not deployment topology.
- Treating economy as a reason to skip maintainability. The book's "programmer time is expensive" rule is a trade-off stated for its time; weigh the current cost of machine time and of maintenance before applying it.

For the scope of the sources and their dated claims, see [sources](references/sources.md). Related disciplines: [modularity](../modularity-principles/SKILL.md) for boundaries, [composition](../composition-principles/SKILL.md) for how parts connect, [interface](../interface-principles/SKILL.md) for user-facing surfaces.
