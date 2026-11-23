---
name: minilanguage-generation-principles
description: Use when deciding whether a problem needs a minilanguage, rules syntax, or template, or whether output should be generated rather than hand-edited. Covers when a language pays for itself. Not a parser-generator guide.
---

# Choose the least powerful language that does the job

A minilanguage lets users express behavior that a fixed program cannot anticipate. It also adds a parser, semantics, documentation, security concerns, and a new way to fail. Before building one, check whether structured data plus ordinary code solves the problem.

## Start with structured data

Prefer a structured data file to a minilanguage that changes external state when interpreted. A data file can be validated, diffed, and reviewed without running anything. Reach for a minilanguage only when the data alone cannot express the required combinations.

## Build a minilanguage only for fluid use

A minilanguage fits when the domain primitives are simple and stable, but the ways users combine them vary widely. If the operations are few and the use is fixed, a function or a table is simpler. Keep the language to the smallest set of constructs that the real uses require.

## Keep generated output traceable

When code or data is generated, push changes into the source of generation rather than editing the output. Keep generated artifacts identifiable and, where possible, regenerate them from the same inputs. A hand-edited generated file will silently lose its edits on the next generation run.

Prefer data-driven logic where the program's behavior can be changed by editing a table. Hand-coded state machines are often rigid where a table would be easy to change. Use generation for repetitive, mechanical output; use hand-written code where the logic is the point.

## Watch for these failure modes

- A minilanguage built for a problem a table or function could solve.
- Users depending on undocumented corner cases of the language.
- Generated files edited by hand, with no record of which edits were intended.
- A minilanguage with no error messages that point to the offending input.
For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [textuality](../textuality-principles/SKILL.md) for the format of the data, [configuration](../configuration-principles/SKILL.md) for settings a user controls, [security](../security-principles/SKILL.md) for trust boundaries around executable input, including embedded execution.
