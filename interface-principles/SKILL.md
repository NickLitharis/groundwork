---
name: interface-principles
description: Use when designing a command-line or function interface: defaults, stdout versus stderr, exit status, discoverability, or scriptability. General interface principles, not HTTP or REST API design.
---

# Design interfaces that do the expected thing

An interface is a contract that users learn once and rely on afterward. Make its behavior predictable, keep its output to what matters, and reuse conventions the user already knows. Every surprising behavior costs the user attention, and attention is the scarce resource.

## Do the least surprising thing

Find the existing programs, libraries, or conventions your users already know, and match the relevant parts. Novelty raises the cost of a user's first use. Mimic familiar behavior unless the new behavior is clearly better and the difference is worth explaining.

This is not a call for mechanical conservatism. A poor interface stays painful for its users, so the goal is to make the first use familiar and the continued use good. Use taste and judgment.

## Keep output to what matters

Print only what the user asked for and what they need to act on. Pipelines and scripts read standard output as data, so a status message there breaks them even when nothing went wrong. Send real errors to standard error, and keep standard output for data.

The same principle applies to visible output in general. Each unneeded line is a cost in attention and context. Progress indicators for long operations are appropriate. Confirmation prompts should appear only when an operation may lose or destroy data.

## Make success and failure distinguishable

A script can react only to what the program reports through its exit status and stderr. Use zero exit status for success and a nonzero status for failure, and document any specific codes the tool promises. Include enough context in the diagnostic to act on the failure, without secrets. Do not promise that piped output is atomic: say whether malformed input can leave partial output. Accept input leniently only through an explicit, documented mode; be generous in what the specification allows, but do not let an implementation silently accept malformed input, because that spreads incompatibility. Details and examples are in [CLI contracts](references/cli-contracts.md).

## Delegate to familiar tools

When a task is better done by a tool the user already knows, let the user choose that tool. A program that needs substantial text entry should call the user's editor rather than embed its own.

## Make interfaces scriptable and inspectable

An interface should behave the same way when a person uses it and when a script calls it. Interactive prompts that block a script, or output formats that change with terminal width, make automation fragile. Where an interface is interactive, offer a non-interactive path with the same results.

## Watch for these failure modes

- Standard output polluted with diagnostics, breaking pipelines.
- Novel command names or flags for operations users already perform with familiar tools.
- Prompts that cannot be bypassed in scripts.
- Errors that do not identify the failing input or the next step.
- Default behavior that changes without notice.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [configuration](../configuration-principles/SKILL.md) for settings that shape the interface, [communication](../communication-principles/SKILL.md) for messages to people, [composition](../composition-principles/SKILL.md) for how interfaces connect.
