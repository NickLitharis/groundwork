---
name: data-modeling-principles
description: Use when defining or reviewing the meaning, identity, invariants, relationships, time semantics, ownership, or representation of data in a domain, API, file, message, database, or analytical model. Helps make important distinctions explicit and choose a shape that fits real consumers. Not a migration/rollout guide or runtime-failure playbook.
---

# Model what the data means

Use this skill when a decision changes what a datum represents, which values are valid, how facts relate, or what consumers may infer. Model across tables, objects, documents, messages, files, events, and views; do not equate the domain model with an ORM or storage schema. Apply only relevant checks. This skill complements—not replaces—other principles skills and is not an all-skills pipeline.

## Make meaning and distinctions explicit

1. Name the concept in the language of its domain and context. Ask a domain owner when terms or rules conflict. State what a record means and what would make two records the same thing.
2. Separate stable identity from mutable attributes. Give identifiers a scope and lifetime: a display name, email, account number, and internal ID may each change or be unique only within a tenant or period. Do not use a mutable label as identity unless the domain guarantees that contract.
3. Write valid and invalid examples, then state invariants: allowed values, uniqueness scope, lifecycle, and relationship cardinality/optionality. Trace which facts determine which others. Repeated facts can create inconsistent updates, but split a relationship into its own concept only when its own meaning, attributes, identity, lifecycle, or history warrants it.
4. For quantities, state unit, scale/precision, range, rounding point and rule, and overflow behavior. For money, identify currency and do not combine unlike currencies without a conversion rule. Choose exact arithmetic when the contract requires it; measured estimates may instead need a tolerance and an inexact representation.
5. Give time a meaning: calendar date, instant, local civil appointment, duration, effective period, or recorded/observed time are not interchangeable. Preserve a zone or other context when future interpretation needs it. Confirm the target platform's actual parsing, storage, conversion, and precision rules.
6. Distinguish absent, unknown, not applicable, withheld, empty, and zero only when consumers or rules treat them differently. Document defaults and omission/null behavior at API and serialization boundaries; avoid inventing states with no observable consequence.
7. Name the authority for each fact and mark computed, cached, indexed, or reporting values as derived. State their inputs, refresh/correction policy, and acceptable staleness. There need not be one authoritative database for every fact.

## Choose the representation for its consumers

Choose tables, records, documents, events, graphs, or projections based on the meaning to preserve, invariants to enforce, and actual read/write patterns. Relational dependency analysis can reveal update anomalies and help decide where facts belong; it is a diagnostic, not a command to normalize every representation. Normalize when shared facts, independent updates, or integrity rules benefit from one authoritative representation. Denormalize when a measured or explicit access need benefits and the duplication has a clear owner, refresh path, and staleness/correction policy. Neither is a universal rule. Event history, current-state snapshots, relational constraints, and flexible documents are options—not defaults.

Check that the chosen shape can express the required constraints, identity, time and missing-value semantics. A database constraint, API validation rule, document schema, or event contract may enforce different parts of an invariant; identify which layer is authoritative and do not assume a type declaration alone enforces the domain rule. Check representative valid and invalid examples at the boundary where data enters and where consumers read it. If the language, database, schema format, or protocol has special behavior, inspect its current documentation and test the edge cases that carry domain meaning; primitive type names alone are not evidence.

Relational-model, integrity-constraint, functional-dependency, and normalization ideas inform checks for domains, relationships, dependencies, and anomalies. Their relational setting does not make SQL normalization a universal model for APIs, documents, events, or views.

## Example

A charge of `10.00` is not a complete monetary fact without a currency and the rules for scale and rounding. A balance of `0` means a known zero; an omitted balance may mean not supplied, and `null` may mean unknown—choose the distinctions the product actually observes. A customer's name can change without changing customer identity. A monthly report may duplicate current customer labels for a useful read, but say whether it shows today's label or the label at the time of each charge.

For deeper worked examples and evidence checks, read [references/modeling-examples.md](references/modeling-examples.md).

## Keep boundaries clear

Modeling establishes what facts mean and what must remain true. For changing already-persisted or published contracts, use [evolution-principles](../evolution-principles/SKILL.md) for compatibility, migration, rollout, and cutover. When concurrent writes, partial failure, retries, or recovery threaten an invariant, use [reliability-principles](../reliability-principles/SKILL.md) for runtime guarantees. Do not turn a modeling decision into a migration plan or a failure-handling prescription.