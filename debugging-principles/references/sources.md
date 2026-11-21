# Sources and Scope

This skill is an original, conditional synthesis. Its links are background and evidence references, not runtime dependencies. It does not require fetching a book or loading another skill.

## Inspected material and boundaries

- Andreas Zeller, *The Debugging Book*, [Introduction to Debugging](https://www.debuggingbook.org/html/Intro_Debugging.html): the sections “A First Fix,” “The Devil's Guide to Debugging,” and the scientific-method discussion were inspected. The chapter teaches preserving behavior and testing explanations; its examples are not controlled evidence that a particular debugging method always improves outcomes.
- Zeller, [Reducing Failure-Inducing Inputs](https://www.debuggingbook.org/html/DeltaDebugger.html): “Manual Input Reduction” and “Delta Debugging” were inspected. Reduction checks candidate simplifications against a failure predicate; a reduced trigger is not necessarily a unique minimum or causal explanation. The described method assumes the failure can be classified by repeated runs; flaky timing requires additional care.
- Zeller, [Isolating Failure-Inducing Changes](https://www.debuggingbook.org/html/ChangeDebugger.html): the `ChangeDebugger` workflow was inspected. A passing version, failing version, and classifying test can narrow changed code; the isolated changes still need causal review, especially when changes interact or environments differ.

These are the portions reviewed for this skill. *Why Programs Fail* and other chapters are not used to support its claims. Inspection bounds follow the project chapter review, dated 2026-11-21; that is the review date, not a claim that the online book was published then. The online text's own citation/version information should be consulted if an edition-specific detail matters.

## Author advice and synthesis

The hypothesis → discriminating prediction → experiment loop, preserving observations, and explaining a fix are paraphrases of Zeller's scientific-method discussion. Input and change reduction are author-described techniques conditioned on a repeatable failure and a useful failure predicate.

Applying these ideas to production-only reports, low-impact instrumentation, timing perturbation, statistical rates, and explicit failed-assumption checks is practical synthesis. It broadens the evidence sources beyond a stable local reproducer; it is not a claim that the book evaluates production debugging or proves these procedures causally effective. A production report can be meaningful evidence while remaining incomplete or uncertain.

## Decision examples and evidence checks

1. **Timeout with uncertain side effect.** Preserve the user report and request/transaction identifier; compare application logs with durable state and provider status before retrying. Why: the absence of a response does not establish that the operation did not commit. Check the transaction ledger and external status rather than relying on a timeout message.
2. **Intermittent race disappears under logging.** Compare low-impact counters or sampled traces with baseline failure rates and retain load, version, and schedule context. Why: instrumentation can alter contention or timing. Check whether the instrumentation itself changes incidence and whether the predicted ordering appears; a disappearing failure is not evidence the race is fixed.
3. **Regression narrowed to a release interval.** Compare revisions using the same scenario, configuration, and dependency versions where feasible, then inspect the candidate change's mechanism. Why: version isolation reduces the search area but cannot rule out interaction or drift. Check both the boundary behavior and the proposed causal path; report remaining confounders.

The examples are applications of the principles, not case studies from the cited books. Where conditions cannot be controlled, state what evidence is correlational and what remains unknown.
