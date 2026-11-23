---
name: modularity-principles
description: Use when splitting a system into components, placing a module boundary, reviewing an interface between parts, or judging whether a module is too thin, too large, or leaks internals. Not a size rule.
---

# Draw boundaries that hide decisions

A module earns its place by hiding design decisions behind a small interface. Judge a boundary by what callers must know, not by how many lines it contains or how many files it occupies.

## Make the interface the design

Modules should communicate through narrow, well-defined interfaces. They should not call into each other's internals or share global state. The interface is the real architecture; the code behind it is an implementation detail that can change.

Test an interface before coding it. Write a plain-language description of what it does. If the description requires code excerpts to make sense, or if it reveals that callers must understand internal state, the boundary is wrong.

## Prefer deep modules

A module's value is the functionality it provides. Its cost to the rest of the system is its interface. A deep module provides a lot of behavior behind a small interface. A shallow module exposes nearly as much complexity as it hides, so it adds a layer without removing much work.

Check whether a new layer adds depth. If a function only forwards its arguments to another function with the same signature, the boundary usually adds cost without benefit. Keep the boundary only if it hides a decision that could change.

Information hiding is the main technique for depth. Each module should encapsulate design decisions such as data layout, algorithm, storage format, or protocol details, and those decisions should not appear in its interface.

## Size modules by their decisions

Splitting a module into many tiny parts multiplies interfaces, and each interface is a cost. The Unix tradition also warns against modules that are too large. One cited study (Hatton) reports that defect density is higher at both very small and very large module sizes. Treat that as a caution to check in your own codebase, not as a sizing rule.

## Keep glue thin

When high-level logic meets low-level primitives, a glue layer is needed to connect them. Keep glue thin. Glue that hides cracks between layers spreads kludges into the boundary and makes both sides harder to understand.

## Watch for these failure modes

- Pass-through modules that add a name but no depth.
- Callers that reach into a module's internal state, bypassing its interface.
- Global data shared between modules as a convenience.
- Glue that grows into a second implementation of one of the layers.
- Splitting for its own sake, producing many small interfaces that each need documentation and tests.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [unix-philosophy](../unix-philosophy-principles/SKILL.md) for responsibility boundaries, [transparency](../transparency-principles/SKILL.md) for how internals stay inspectable, [composition](../composition-principles/SKILL.md) for how modules run together.
