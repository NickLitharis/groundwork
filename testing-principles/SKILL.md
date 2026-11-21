---
name: testing-principles
description: Use when choosing or improving tests for software behavior, a bug fix, a new contract, a flaky suite, generated inputs, or a risky boundary. Focus on independent oracles, meaningful case selection, appropriate test boundaries, and honest interpretation of evidence. Complements project test workflows; not a mandate to write tests for unrelated prose or to use one testing method everywhere.
---

# Testing Principles

A test is useful when it checks behavior that matters against an oracle independent enough to catch a mistake. Treat a passing suite as evidence about assertions and executions performed—not proof of correctness. Choose tests to reduce relevant uncertainty and protect contracts, with effort proportionate to risk and change.

## Choose the oracle and cases

- **Start from the contract, not the implementation.** Identify the promised result, invariant, error, or side effect from requirements, public behavior, or an authoritative owner. Deriving expected output only from current code can encode its bug. Resolve materially ambiguous requirements rather than pretending a test can supply the missing specification.
- **Partition behavior with a reason.** Select representative examples for distinct paths, equivalence classes, state transitions, and interactions. Examine boundaries where behavior changes: empty/full, just inside/outside a limit, invalid forms, and transitions between states. Do not multiply cases mechanically; select the ones likely to reveal a contract violation.
- **Use examples for named expectations and incidents.** Keep concrete cases for important boundary values, regressions, and domain exceptions. Examples make expected behavior legible and preserve specific known failures.
- **Use properties when the general relation is clear.** A property can explore many inputs, but the generator must produce meaningful valid cases and the oracle must express a justified invariant. Check generator validity, distribution, and shrinking; a broad generator full of invalid values or a tautological property can create false confidence. Retain examples for special cases and known incidents.
- **Make generated failures replayable.** Preserve the failing input and seed where applicable. A shrinker should keep the target failure, not merely any failure. Random sampling can find counterexamples but cannot establish that rare cases are absent.

## Select test boundaries

- **Test stable, meaningful behavior rather than private structure by default.** Prefer the narrowest observable contract that represents what a caller relies on. A language-level public API is not always the right boundary; avoid exposing internals solely to make tests possible. Assertions about interactions are appropriate when the interaction itself is contractual, but call sequences that merely mirror implementation make refactors brittle.
- **Choose real dependencies or doubles for a reason.** Real components provide evidence about actual integration when they are sufficiently fast, deterministic, and safe. A fake, stub, or mock can isolate a boundary that is costly, unavailable, nondeterministic, or outside the unit's responsibility. Keep the double faithful to the relevant contract and add integration checks where real serialization, persistence, protocol, or service behavior matters. A mock-only green result does not validate that boundary.
- **Control state and ordering where they affect behavior.** Tests that depend on shared state, wall-clock timing, parallel order, network services, or uncontrolled randomness can fail for reasons unrelated to the contract. Prefer isolation and explicit dependencies when practical. For intermittent failures, preserve timestamps, environment, seeds, and run outcomes; statistical investigation of failure rates can be informative even when a single deterministic replay is unavailable. Do not relabel a flaky failure as harmless without evidence.

## Interpret test evidence

Coverage shows what executed, not whether the oracle would detect a wrong result. Mutation analysis can probe whether assertions react to selected artificial changes, but its score depends on the mutants and assumptions about how they represent faults; it is not a direct estimate of real defect detection. A green test says the checked assertions held for those executions under that environment and test data.

Test-driven development is one feedback technique, not a universal entrance requirement. Consider test-first increments when desired behavior is clear, an independent oracle is available, and feedback is cheap. If the problem is exploratory, requirements are unsettled, or behavior is difficult to observe at first, investigate or prototype before committing to a test interpretation; then add appropriate behavior checks. TDD does not remove the need to test broader boundaries or failure modes.

Scale effort to impact. A localized deterministic change may need a focused contract check; persistence, concurrency, compatibility, or security changes may need multiple boundaries and failure conditions. Reuse adequate existing evidence instead of adding redundant tests. Keep test selection tied to the behavior changed, not a universal coverage target.

## Examples

- A discount function has a published rule “10% off orders of at least $100.” Test representative values below, at, and above the threshold, plus rounding and excluded products if the contract defines them. Check expected results against the approved rule, not an implementation helper reused by the test. This catches off-by-one behavior without enumerating every price.
- A JSON adapter passes unit tests using a mock transport, but deployed consumers reject its payload. Keep unit tests for mapping logic, then add a focused integration check against the real serializer/schema or service contract. Verify the emitted bytes/fields and rejection behavior; mock success cannot establish wire compatibility.
- A parallel test fails intermittently after a shared cache was introduced. Track failure counts with and without the cache, order, worker count, and relevant schedules; compare against an isolated run and inspect whether outcomes cluster under a particular interleaving. A rate shift is evidence of association, not by itself proof of cause; validate the synchronization mechanism and replay when possible.

## Keep principles distinct from procedures

This skill helps choose or interpret tests; it does not dictate a runner, exact test pyramid, report format, or mandatory test-first process. Use `ds-tdd` for its specific test-driven workflow and `ds-verify-loop` for verification after changes. `engineering-principles` addresses broader design and implementation decisions. These operational workflows complement rather than replace contract-based judgment.

