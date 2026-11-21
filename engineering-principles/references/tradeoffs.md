# Resolving Competing Principles

Start from requirements and concrete costs. Identify the simplest candidate, the risk it leaves exposed, and whether additional structure actually reduces that risk. Explain only the tradeoff that changes the decision.

## DRY versus independent change

Two calculations both multiply a price by a rate: one estimates shipping, the other computes tax. Similar syntax is not a shared domain rule. Keep them separate if legislation and shipping policy change independently. Share a genuine unit-conversion or rounding rule only when its semantics are identical.

Conversely, two endpoints enforcing the same permission policy should share an authoritative policy implementation. Fixing only one copy leaves inconsistent authorization.

## YAGNI versus safe extensibility

A CSV export is required today; a plugin registry for possible PDF and XML formats is not. Implement CSV through a cohesive function using an existing encoder. Preserve a clean call boundary so another format can be added later without pretending it already exists.

YAGNI does not mean concatenate CSV strings without escaping, omit an authorization check, or ignore a stated memory limit. Those are present correctness requirements.

## Single responsibility versus wrapper sprawl

A client that owns authentication, request transport, pagination, and error mapping for one external service can be cohesive. Splitting every operation into a one-method class may distribute the same complexity across more files. Separate independently changing policy or resource ownership, not every individual verb.

## Refactoring versus behavior change

A legacy serializer returns an empty string for a missing value. During a readability refactor, preserve that result and protect it with existing or characterization tests. Changing it to null is a separate contract decision requiring consumer analysis and updated expectations. Do not hide the change behind the claim that null is cleaner.

## Silence versus observability

A pipeline command should not print "Done!" to stdout, because downstream parsers consume that stream. It should still emit the requested records, report errors to stderr, and return a meaningful status. A service may need structured operational logs and metrics even when its CLI counterpart is quiet.

## Fail fast versus resilience

Reject invalid configuration before accepting work. For a documented transient network failure, a bounded retry can be appropriate if the operation is safe to repeat and respects deadlines. Retrying every error, swallowing failures, or returning empty data makes the system less reliable. Do not add retries without a requirement or evidence that the failure is transient.

## Simple implementation versus performance constraints

For a small bounded dataset, a direct scan may be clearer than an index. For a large stream under a memory cap, loading everything first is not a valid simple solution. Choose an algorithm that meets the stated bounds, then measure before adding clever optimizations.

## Composition versus process boundaries

A parser and renderer can compose through in-process values; they do not need a message broker or separate services. Use text streams when interoperability and inspection help. Use a binary format or library API when exact data fidelity, throughput, or resource constraints justify it.

## Compatibility versus coordinated change

A private function and its only caller can often change in one patch. A public SDK used by independently deployed consumers may need deprecation and staged migration. Do not apply mandatory compatibility shims to the former or a destructive clean cutover to the latter.
