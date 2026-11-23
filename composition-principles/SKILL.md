---
name: composition-principles
description: Use when designing programs or components that must work together, choosing between pipelines, filters, wrappers, subprocess calls, interactive child processes, sockets, or RPC, or deciding which side owns control flow and protocol state. Not a guide to shell scripting syntax or to any particular message broker.
---

# Connect parts with the least coupling that works

Programs that compose well can be tested, replaced, and reused independently. Before choosing how two parts communicate, state what each owns and how much they must know about each other. Choose the simplest mechanism that meets the contract.

## Design for connection

Build components to be connected to other components. The standard streams convention, in which a program reads input and writes output without knowing its neighbors, is the simplest example. A filter that reads one stream and writes another can be inserted into a pipeline, tested alone, and replaced without changing its neighbors.

## Rank the mechanisms by coupling

Use the least coupled mechanism that handles the work:

- **Shellout or pipeline**: one-way data flow, with no protocol during execution. Lowest coupling. Prefer it when the input is known in advance and the output is the result.
- **Wrapper**: a thin layer that calls another program with fixed arguments to change its behavior. Use it to hide a complicated invocation, not to add logic.
- **Interactive slave process**: two-way exchange through a child process's standard streams. Both sides need a state machine to avoid deadlocks and races. This is harder to test and debug than a shellout. Use it only when the protocol is trivially simple, or when the child speaks a proper application protocol.
- **Client and server over a protocol**: separates responsibilities and lets each side change independently, at the cost of a defined protocol and handling of network failure. The book cites a database split into client and server as a way to hold complexity down.

## Make the connection debuggable

When a program calls another as an interactive child, let callers override the child command with a switch or environment variable. That allows the real child to be run under a logging harness during development.

Keep the protocol as small as possible. Each message type, field, and state transition is a source of misunderstanding and a place where both sides can disagree.

## Choose boundaries by responsibility

Temporary files, sockets, shared memory, and RPC are closely equivalent in what data they can move. The differences are at the edges: how the two sides establish contact, who serializes and parses messages, how buffering behaves, and what atomicity the messages have. Choose a mechanism based on those edge properties, not on which one is most fashionable.

## Watch for these failure modes

- Interactive child processes with no protocol definition, leading to deadlocks when one side waits for output the other has not produced.
- Pipelines that fail silently when an early stage exits, leaving downstream stages to process partial input.
- Wrappers that grow logic until they are a second implementation.
- Mixing data exchange and control flow in one channel, so neither can be reasoned about separately.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [unix-philosophy](../unix-philosophy-principles/SKILL.md) for component responsibilities, [textuality](../textuality-principles/SKILL.md) for the data that moves, [reliability](../reliability-principles/SKILL.md) for timeouts and partial failure across processes.
