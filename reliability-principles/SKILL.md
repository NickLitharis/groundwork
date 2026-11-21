---
name: reliability-principles
description: Use when designing or changing services, jobs, APIs, or stateful systems where partial failure, timeouts, retries, overload, concurrency, or recovery can affect user outcomes. Helps set fit-for-purpose reliability objectives and bound failure handling. Not a mandate to add distributed-systems machinery to a local script or to replace operational runbooks.
---

# Make reliability claims testable

Use only the parts that match the system's failure modes. A script with no concurrent callers or remote side effects may need clear error handling and a backup, not retry budgets, circuit breakers, or a queueing architecture. This skill complements established SRE, incident, and domain-specific procedures; it is not an all-skills pipeline.

## Define the outcome and invariants

Start from user-visible outcomes: availability, latency (including tail behavior when relevant), correctness, and durability. Choose a small number of indicators and a target that reflects user, product, contractual, legal, and safety needs. Do not copy a target from current performance or treat 100% as a universal goal.

Separate a probabilistic service objective from hard invariants. A budget for occasional latency or availability failures must not silently permit corrupted balances, unauthorized actions, privacy violations, or safety/legal violations. State which outcomes may degrade and which must remain true.

Trace important operations through their state boundary: what is read or written, which dependencies participate, what is atomic, and what the caller can observe. A timeout is an unknown outcome when the remote operation may have committed. Do not turn “no response” into “no effect.”

## Bound retries and resource use

Retry only failures that could plausibly improve and only when the operation can safely be repeated or its outcome can first be resolved. Mutations need a deliberate idempotency/deduplication contract. Define the operation identity, payload binding (reject conflicting reuse), scope of the guarantee, and retention period relative to retries, message delay, and replay. Couple the record and state mutation atomically where feasible. “Exactly once” applies only to a specified boundary whose participating systems enforce it; it is not an end-to-end promise for arbitrary external effects.

Use a total deadline and bounded retry budget, not an unbounded loop at every layer. Backoff with jitter can reduce synchronized retries, but retries add load and may worsen overload. Choose one appropriate retry point or a coordinated local budget for the architecture; avoid multiplication across layers. After a deadline or ambiguous commit, query status, reconcile, or expose uncertainty instead of blindly repeating a side effect.

Bound concurrent work and queued work when overload can exhaust resources or make deadlines useless. Apply backpressure, shed or defer work, or degrade noncritical functions only when the user and safety contract permits. Queue limits and load signals should reflect resource cost, not just request count. Do not introduce a queue, circuit breaker, or distributed coordinator without a concrete failure mode it addresses.

## Preserve state and recover from damage

Protect state transitions against races and partial writes. Use a transaction, compare-and-set/version check, unique operation identity, or simpler single-writer design when concurrent mutation is possible. Make the boundary and guarantees explicit; a local atomic file replace may be enough for a local tool.

Treat recovery as a capability to demonstrate, not an assumption based on replicas or backup jobs. Replication can copy corruption or deletion. Decide acceptable data loss and restoration time where relevant, preserve needed history, and exercise restore/reconciliation—including corruption or mistaken deletion when plausible. A backup that has not been restored is an unverified recovery claim.

Plan for corruption detection and safe repair where data integrity matters. Do not recommend soft deletion where deletion obligations, privacy, retention, or resource cost make it wrong. Recovery and rollback do not undo external effects automatically; identify an actual compensating action or a forward-repair path.

## Check proportionately

Test the failures that matter to this operation: timeout before and after commit, duplicate delivery, conflicting idempotency-key reuse, retry exhaustion, simultaneous updates, queue saturation, partial dependency outage, corrupted input/state, and restore—selecting only those applicable. Check that bounded work terminates within the deadline and that retry behavior does not amplify failure.

Operational measures should expose user outcomes and actionable failure signals without hiding uncertainty. Exercise rarely used fallback/degradation paths if they are part of the reliability claim. Report untested assumptions plainly; successful happy-path checks do not prove durability or recovery.

## Decision examples

- **A local report-generation script reads one file and writes one output.** No concurrent requests or remote mutation exist. Prefer clear failure reporting and safe output replacement; do not add a circuit breaker or distributed idempotency store. Check: interrupted-write behavior and whether a rerun leaves a valid output.
- **A payment API times out after submitting a charge.** The charge may have committed. Reuse a durable operation identity bound to the request, check status or reconcile after timeout, and retry only under the provider's idempotency contract and retention window. Check: timeout-after-commit and conflicting key payload behavior; do not assume rollback reverses a charge.
- **Workers fall behind during a dependency outage.** Unbounded queues and nested retries may turn a transient outage into overload. Bound concurrency/queue growth, deadlines, and a shared retry budget; defer or shed work only if product invariants permit. Check: saturation behavior, recovery rate, and whether retry load remains bounded.

