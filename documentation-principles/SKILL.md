---
name: documentation-principles
description: Use when writing or reviewing documentation, deciding what to document, or organizing docs by reader need: tutorial, how-to, reference, or explanation. Also covers agent-facing project docs. Not a toolchain guide.
---

# Organize documentation by the reader's need

Documentation fails when it mixes forms: a tutorial that stops to list every option, or a reference page that tries to teach. Before writing, decide which need the document serves, then write it in that form. Keep documentation close to the code it describes, and keep it accurate.

## Know the four needs

Diátaxis identifies four distinct needs and four corresponding forms:

- **Tutorials**: learning by doing, guided from a starting point to a working result. The reader is a learner.
- **How-to guides**: directions for a specific task. The reader already knows the basics and needs to get something done.
- **Reference**: accurate, complete descriptions of the interface, arranged for lookup. The reader needs a fact.
- **Explanation**: discussion of why things are the way they are, for understanding. The reader is trying to build a mental model.

Each form has a different job. Put content in the form that matches the reader's current need, and link between forms rather than merging them.

## Make reference complete

For Unix tools, the manual page remains the most important form of reference documentation. Treat the reference for each command, function, or endpoint as a required deliverable, not an optional extra. Its content should include defaults, error conditions, and units. Writing an interface description before coding it is owned by [modularity-principles](../modularity-principles/SKILL.md).

## Write explanations that show the mechanism

An explanation starts with what the piece of code is for, then ties that purpose to this codebase: what happens when someone uses it, why it has its current shape, and which edge cases matter. The reader is building a mental model of code they will change. Pick the three or four things the reader should leave knowing, and skip what they already know. Cite the file and line for every claim about behavior.

Separate what the record says (commit messages, pull requests, linked issues, nearby comments) from what you infer. Label inferences as inferences. If no record explains a choice, say the reason is unknown rather than presenting a guess about intent as fact. Explain ideas rather than listing functions.

## Keep documentation honest

Documentation should describe current behavior. When behavior changes, update the document in the same change. A tutorial that no longer runs, or a reference that lists options the program no longer accepts, is worse than no document, because it misleads the reader.

## Write agent-facing project docs

A project's agent instructions file (such as a CLAUDE.md) should contain what an agent cannot cheaply learn from the code: the commands that build, test, and run the project; the layout of the codebase; non-obvious patterns and gotchas; and how the project's tests and deploy steps are run. Keep each entry short and executable. Leave out generic best practices, facts the code states plainly, and one-off fixes unlikely to recur. Check that each instruction still matches the codebase, since a stale command is worse than none.

## Watch for these failure modes

- A single long page mixing learning, task steps, and lookup tables.
- Reference content that omits defaults, error conditions, or units.
- Explanation buried inside a how-to, so the task steps are hard to find.
- Documentation that describes intended behavior rather than actual behavior.
- Documentation maintained separately from the code, so it drifts.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [interface](../interface-principles/SKILL.md) for the interface being documented, [evolution](../evolution-principles/SKILL.md) for documentation of changing contracts, [testing](../testing-principles/SKILL.md) for checking that examples still work.
