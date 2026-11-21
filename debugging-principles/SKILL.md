---
name: debugging-principles
description: Use when diagnosing a software failure, regression, intermittent incident, or unexplained behavior. Preserve reported evidence, compare causal hypotheses with discriminating predictions, and choose experiments that fit the available evidence. Especially useful when logs, production observations, version history, timing, or a stable reproduction offer different investigative paths. Complements debugging tools and workflows; not for ordinary implementation or test design alone.
---

# Debugging Principles

Debugging is explanation-seeking, not just making a symptom disappear. Treat observations as evidence, distinguish them from assumptions, and scale investigation to impact, uncertainty, and the evidence available. A user report or production observation is real evidence; do not require a local reproduction before taking it seriously.

## Reason from evidence

1. **Preserve the reported failure and intended behavior.** Keep the original error, inputs, relevant environment/version, timing, and sequence when available. Record what should have happened separately from what did. Do not replace the report with a simplified case that may have removed the trigger.
2. **List plausible explanations, not just a suspect location.** Connect each candidate mechanism to the observed behavior. A stack frame, recent commit, or failing assertion identifies where to look, not necessarily why the system violates its contract.
3. **Derive a discriminating prediction.** Ask what should differ if one hypothesis is true rather than a plausible alternative. Prefer observations that could disconfirm the favored explanation.
4. **Choose a proportionate experiment.** Inspect relevant code/configuration, compare known-good and failing conditions, add narrowly scoped instrumentation, run a controlled probe, or request missing information only when it materially changes the next step. Record what the experiment can and cannot establish; update hypotheses when results disagree.
5. **Explain the mechanism before calling it a cause.** Show how the condition produces the failure and why that conflicts with intended behavior. A fix passing one example is useful evidence, not proof that the explanation covers all affected cases.

A stable reproducer is valuable when it can be obtained, but it is not a gate to diagnosis. For a production-only fault, a user report, logs, traces, metrics, version comparisons, or a schedule-correlated pattern may support useful investigation. State uncertainty rather than inventing a reproduction.

## Match techniques to conditions

- **Reduce an input only when the target failure is recognizable and repeatable enough.** Remove or simplify parts while checking that the same failure remains. A smaller trigger is a clue, not necessarily the unique minimum or explanation. With intermittent behavior, preserve the seed, schedule, environment, external state, and outcome definition as far as possible. If repeatability is probabilistic, report observed rates and do not claim causal minimization from a run that may have lost or changed the failure.
- **Use version isolation when a passing and failing revision can be compared under a sufficiently consistent test and environment.** The isolated change narrows investigation; interactions, multiple causes, configuration drift, or changed dependencies can invalidate a simple culprit assumption. Inspect how the change creates the observed behavior before attributing cause.
- **Instrument to answer a question.** Select signals tied to competing hypotheses and avoid collecting unrelated sensitive data. Instrumentation can perturb timing, load, locking, or scheduling; compare against uninstrumented observations and preserve the original failure evidence. If measurement changes the result, treat that as evidence about sensitivity, not proof of absence.
- **Check failed assumptions.** When an experiment contradicts expectations, verify its setup, assumptions, and measurement path before discarding the result. Then revise the hypothesis or identify what remains unknown; do not silently tune the experiment until it agrees.

## Examples

- A customer reports a payment timeout but the dashboard shows no local error. Preserve the report and transaction identifier; inspect service and provider timelines and whether the request may have committed before timing out. This can distinguish a lost response from a rejected payment without asking for a repeat charge. Check provider status and ledger state; do not infer “not committed” from the timeout alone.
- A race occurs only under load, and verbose logging makes it disappear. Keep the original timing and load observations; compare low-impact counters or trace sampling against the uninstrumented run, then test a specific ordering hypothesis. Check whether the symptom rate changes with instrumentation and whether the predicted ordering is observed. Logging suppression is not a fix.
- A regression appears between two releases. Run the same valid scenario against both with configuration and dependencies held as constant as practical. A narrowed commit range directs review, but a feature interaction or environment change may be causal. Check the suspected mechanism in code and verify the intended contract with a targeted behavior check.

## Keep principles distinct from procedures

This skill guides how to reason about a failure; it does not require a fixed report, a mandatory reproducer, or a particular debugger. Use repository-specific diagnosis workflows when they fit: `ds-unstick` helps after repeated failed fixes, while `engineering-principles` covers broader implementation choices. Neither a narrowed diff nor a successful test alone establishes root cause.

