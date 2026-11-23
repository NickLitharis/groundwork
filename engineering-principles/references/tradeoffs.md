# Resolving Competing Principles

Start from requirements and concrete costs. Identify the simplest candidate, the risk it leaves exposed, and whether additional structure actually reduces that risk. Explain only the tradeoff that changes the decision.

This reference covers three design conflicts that belong to engineering. Other conflicts are owned by their skills: refactoring versus behavior change by [evolution-principles](../../evolution-principles/SKILL.md), silence versus observability by [communication-principles](../../communication-principles/SKILL.md) and [transparency-principles](../../transparency-principles/SKILL.md), retries versus fail-fast by [reliability-principles](../../reliability-principles/SKILL.md), composition versus process boundaries by [composition-principles](../../composition-principles/SKILL.md), and simplicity versus performance by [performance-principles](../../performance-principles/SKILL.md).

## DRY versus independent change

Two calculations both multiply a price by a rate: one estimates shipping, the other computes tax. Similar syntax is not a shared domain rule. Keep them separate if legislation and shipping policy change independently. Share a genuine unit-conversion or rounding rule only when its semantics are identical.

Conversely, two endpoints enforcing the same permission policy should share an authoritative policy implementation. Fixing only one copy leaves inconsistent authorization.

## YAGNI versus safe extensibility

A CSV export is required today; a plugin registry for possible PDF and XML formats is not. Implement CSV through a cohesive function using an existing encoder. Preserve a clean call boundary so another format can be added later without pretending it already exists.

YAGNI does not mean concatenate CSV strings without escaping, omit an authorization check, or ignore a stated memory limit. Those are present correctness requirements.

## Single responsibility versus wrapper sprawl

A client that owns authentication, request transport, pagination, and error mapping for one external service can be cohesive. Splitting every operation into a one-method class may distribute the same complexity across more files. Separate independently changing policy or resource ownership, not every individual verb.
