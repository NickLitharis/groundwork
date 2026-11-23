---
name: transparency-principles
description: Use when designing a component to be inspected, debugged, or maintained: how much abstraction to place over data, keeping a failure's origin visible in code, or whether a dependency is live. Not observability tooling.
---

# Make behavior visible

Software that is transparent can be inspected while it runs, debugged when it fails, and modified by someone who did not write it. Transparency is a design property. It does not come from documentation added later.

## Keep the path to the thing visible

Avoid layering more abstraction than the problem needs over the data a program manipulates. Abstractions help remove assumptions, but they can also hide the problem being solved. When debugging, a designer who has built many conceptual layers often has trouble seeing what the code actually does. Prefer a representation that a reader can follow directly.

Keep glue layers thin. Glue that adapts between layers should not hide the seams between them, because those seams are where failures appear.

## Keep failures visible

In code, a failure should keep its origin. The error should name the step that failed and carry the state it left behind, so whoever diagnoses it can see the original fault. A handler that swallows an error and continues on partial state moves the fault to a later step, where its cause is hard to find. Which failures to recover from, and how to recover, belongs to [reliability-principles](../reliability-principles/SKILL.md). How an agent reports a failure to a person belongs to [communication-principles](../communication-principles/SKILL.md).

## Judge maintainability by live development

Ask whether a dependency or tool is live, dormant, or dead. Live code has an active maintainer community. Dormant code may be hard to change because its maintainers stopped. Dead code is often easier to replace than to maintain. Apply this when choosing dependencies or deciding what to keep.

## Watch for these failure modes

- Abstractions that hide the cause of a failure from the person debugging it.
- Repairs that hide errors, so later steps proceed on bad state.
- Hand-maintained data mixed with generated or internal state, so readers cannot tell which is authoritative.
- Components that are opaque to their own maintainers.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [textuality](../textuality-principles/SKILL.md) for editable formats, [debugging](../debugging-principles/SKILL.md) for finding causes, [reliability](../reliability-principles/SKILL.md) for recovery at runtime.
