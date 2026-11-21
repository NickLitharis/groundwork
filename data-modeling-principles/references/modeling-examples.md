# Worked data-modeling examples

These examples are reasoning prompts, not prescribed schemas. Identify the domain contract first; the same shape may be right in one context and wrong in another.

## 1. Identity, labels, and relationship meaning

Suppose a tenant manages people who can sign in. A person's email can change, and two tenants may each have a person with the same email. If the product treats a person as the same account after an email change, email is a contact attribute—not that person's stable identity. A key could be unique only within a tenant if all consumers carry tenant scope; globally unique keys may be useful if records cross tenant boundaries. State that scope explicitly and test duplicate-email, email-change, and cross-tenant lookup cases.

A membership between a person and a team may have a role, start/end dates, or its own approval status. If those facts are about the association, not either endpoint alone, model membership as a concept with those attributes. If the relation is merely an unqualified link and has no separate rules, a simpler relationship may suffice. Check whether the real domain permits zero, one, or many memberships and whether one person can hold multiple roles.

**Evidence check:** ask the domain owner what remains the same across rename, merge, re-invitation, and tenant transfer. Inspect actual uniqueness and key constraints in the chosen persistence layer; a label that looks unique in sample data is not proof of a domain invariant.

## 2. Units, money, and precision

A field named `amount: 12.5` is ambiguous: currency or a physical unit? Is 12.5 exact, rounded for display, or an estimate? Does the value allow negatives? For an invoice line, one possible fact is `(amount, currency)` with explicitly defined decimal scale, rounding point/mode, and allowed range. If fractional minor units or tax apportionment matter, define those rules rather than assuming a fixed two-decimal currency. For scientific readings, binary floating point may be appropriate if the model also states measurement units, calibration context, and error tolerance.

For example, `USD 10.00` and `EUR 10.00` are not interchangeable values. Do not sum them as though a numeric addition preserves meaning; specify the conversion source, rate time, and rounding policy if conversion is part of the domain. Preserve the original amount/currency when a later conversion is derived and users or auditors need to understand the original fact.

PostgreSQL 19 documents `numeric` as exact and floating-point types as inexact; declared `numeric` scale rounds inputs, while PostgreSQL `money` fractional precision depends on locale. This is an implementation example, not a universal type recommendation. Check the target runtime's decimal behavior, wire format, database mapping, serialization, rounding ties, and range. Test boundary values, repeated arithmetic, round-trip serialization, and conversion—not just ordinary values.

## 3. Missing, unknown, zero, and empty

Consider an application that collects a household's monthly income. A known value of `0` differs from an unanswered question. “Not applicable” may differ from “not yet collected” if workflows or reports respond differently. “Withheld” may carry a privacy meaning. Do not collapse these states if policy or consumer behavior depends on them; do not create a status enum for distinctions no one observes.

At a JSON boundary, a missing property and a present `null` are distinct representations, and schema rules determine whether either is valid. JSON Schema's object reference says properties are optional unless listed in `required`; PostgreSQL comparison operators involving SQL `NULL` can yield unknown, not ordinary true/false. Those facts illustrate why defaults and null behavior must be checked in each format and implementation. They do not define one universal cross-layer meaning for null.

**Evidence check:** enumerate actual producer inputs and consumer behavior for omitted, null, empty string/list, false, and zero. Test each input through validation, persistence, API serialization, and reporting. Keep only distinctions that change valid behavior, audit meaning, or an explicit contract.

## 4. Time: fact, event, and current state

A birthday is a calendar date, not midnight UTC. “Appointment at 09:00 in Paris” is a local civil time whose intended zone matters; “payment accepted at this instant” is an instant. A duration of 24 elapsed hours is not always the same as advancing one local calendar day across a daylight-saving transition. Name timestamps by what they represent (`occurred_at`, `received_at`, `effective_from`) rather than using an ambiguous `timestamp` label.

An event can express an occurrence and its context, while a current-price field answers what the system currently considers the price. If an event envelope has identifiers such as `source` and `id`, define its identity and payload meaning; do not infer that the feed is complete history, replayable, or authoritative just because it is called an event. Keeping events and current state can be useful, but state which fact source is authoritative, whether a projection can be rebuilt, how corrections are represented, and which time ordering matters. Do not choose event sourcing just because history is useful: a small audit trail or retained prior values may satisfy the need. Conversely, a mutable current-state value cannot answer a historical question unless that history is preserved elsewhere.

PostgreSQL documents that `timestamp with time zone` is stored in UTC and does not retain the originally supplied zone. If future civil-time interpretation needs the named zone, store that context separately. Verify the language and database rules around ambiguous/nonexistent local times and changing time-zone databases.

## 5. Normalization, projections, and real access patterns

A catalog item has one current description and many orders. Under the rule “item ID determines the current description,” copying that current description into every order repeats a fact and permits inconsistent edits; keeping one current catalog description avoids that update anomaly when orders need only the current description. But an order receipt may need the description as sold, even after the catalog changes. That order-line snapshot is a different historical fact with its own meaning, not accidental duplication. State which dependency and time interpretation apply before choosing what to share or snapshot.

A dashboard may precompute daily totals to avoid repeatedly aggregating a large ledger. That projection is justified by an actual query/latency or cost need, not by a general preference for denormalization. Document the source facts, calculation/version, refresh cadence, acceptable lag, and rebuild or reconciliation method. If reports require exact close-of-day figures, define the cutoff time zone and correction behavior. A cache or materialized view is not automatically authoritative because it is fast.

A relational schema, a JSON document, and a key-value record can each represent the same domain with different constraint and query affordances. PostgreSQL JSONB supports indexes for selected operators and has different semantics from preserving input JSON text; a document may fit cohesive, mostly atomic data, while independently queried or constrained facts may need separate structures. An API schema can specify required properties, but its rules need not enforce every cross-record invariant; an event contract may define occurrence and context without saying how to maintain current projections. The workload, invariants, update independence, and consumers decide. Use dependency/anomaly analysis to expose risks, not as a requirement to normalize every non-relational representation.

**Evidence check:** list the important reads and writes with realistic cardinality and data volume; identify which fields are filtered, joined, sorted, aggregated, or updated independently. Use representative query plans, timings, contention observations, and integrity checks when performance is the reason to duplicate or reshape data. Verify that any optimization still preserves domain meaning and has a known source of truth.