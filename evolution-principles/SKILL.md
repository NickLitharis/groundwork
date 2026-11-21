---
name: evolution-principles
description: Use for behavior-preserving refactors, API or schema changes, data migrations, deprecations, and rollouts involving existing consumers, stored state, or multiple versions. Distinguish structural changes from intentional contract changes and reason about compatibility, cutover, and recovery. Not a general implementation skill or a substitute for repository-specific migration and release procedures.
---

# Evolve software without confusing code cleanup with contract change

Use this skill when a change must coexist with deployed code, stored data, clients, workers, or queued work. For a local, isolated change with no relevant existing contract, apply only the relevant principles. This skill complements—not replaces—domain-specific release, migration, and review workflows. Do not load every principles skill as a pipeline.

## Decide what kind of change this is

1. Identify the need and the boundary that must remain stable: observable behavior, public API, persisted data, event/message shape, operational behavior, or a combination.
2. Classify the work:
   - **Refactoring** changes internal structure while preserving the relevant behavior and contracts.
   - **Intentional contract change** changes what a consumer may observe or rely on. Name the affected consumers and the migration or compatibility decision.
   - **Both**: separate structural steps from behavior/contract steps where that makes review and diagnosis clearer; do not conceal a breaking change under “refactor.”
3. Decide whether structural change is worth doing now. If it makes a known upcoming change safer or simpler, a small behavior-preserving step may help. If the code is stable, understandable, and not blocking a real need, leave it alone. General cleanup has a cost too.
4. Pick evidence that reaches the affected boundary. Existing tests can characterize observed behavior, but they may omit undocumented consumers, timing, error cases, data meaning, or external side effects. Treat characterization as a map of sampled behavior—not proof that all behavior is desirable or captured.

## Preserve contracts across the actual transition

For a rollout that can expose mixed states, enumerate which versions and data shapes can meet: old/new binaries, API clients, workers, delayed or replayed messages, and old/new schemas. Check the combinations that are possible in this deployment, not every imaginary combination.

When consumers cannot switch atomically, additive expansion followed by migration and eventual contraction can reduce incompatibility: first make readers/writers tolerate both forms, move or rewrite data and consumers, verify old usage has ended, then remove the obsolete form. Use this pattern when the deployment actually has an overlap window or delayed consumers. A feature flag alone does not make incompatible versions compatible. Do not impose a three-release schedule or expand/migrate/contract ceremony on a truly atomic, single-consumer change.

Before removing a field, route, event variant, or old reader, check real usage, queued-message lifetime, retry/replay behavior, data backfill completeness, and any external clients that are not under the deployer's control. Set a concrete condition for contraction (for example, no old reads during a measured window and all retained messages understood), appropriate to the system.

## Plan cutover and recovery honestly

Separate deployment rollback from data rollback. Reverting a binary may work while persistent state remains compatible; it may not restore deleted or transformed data, revoked keys, emitted messages, or effects committed by an external service. Before a destructive cutover, decide what recovery means: reverse migration, restore, reconciliation, compensating action, or forward repair. If none can undo the effect, make that limitation and the forward-recovery path explicit.

Do not prescribe a compatibility shim by default. Keep one only when it serves a known active consumer or a bounded migration need; remove it when its retirement condition is met. Likewise, “small steps” should keep changes understandable and recoverable without fragmenting a coherent migration into unsafe partial states.

## Check the result

Choose checks based on the boundary changed: behavioral characterization for a refactor; contract tests or consumer evidence for an API/message change; migration tests on representative prior data; mixed-version or replay checks when those states can occur; and post-cutover observations before destructive cleanup. Green local tests are useful evidence, not a guarantee of external compatibility.

For a refactor, compare relevant before/after behavior and keep a recoverable working state. For a contract change, verify the new contract and the transition path, including failure and rollback/roll-forward conditions. Record the uncertainty that remains rather than claiming compatibility from a test suite that did not exercise it.

## Decision examples

- **Rename a private helper to make an upcoming change easier.** If behavior and external boundaries remain unchanged, keep the refactor local and run the relevant behavior checks. Do not expand it into unrelated cleanup. Check: focused tests plus review that no public symbol or serialized name changed.
- **Remove a database column during a rolling deploy.** Old workers may still write it and queued jobs may run later. Add compatibility first, migrate and observe old use, then contract only after the actual consumers are gone. Check: old/new code against intermediate schema, migration completion, and delayed-job handling. A fixed number of releases is not the criterion.
- **Change an event consumed by an independently deployed partner.** This is a contract change, not a refactor. Preserve old-reader compatibility or coordinate a cutover under an agreed support window; do not assume a code rollback reverses already published events. Check: consumer contract evidence and a defined recovery or forward-fix plan.

