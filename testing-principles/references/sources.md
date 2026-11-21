# Sources and Scope

This skill is an original, conditional synthesis. References support specific ideas below; they are not runtime dependencies, and the agent need not fetch them to apply the skill.

## Inspected material and boundaries

- Maurício Aniche, *Effective Software Testing: A Developer's Guide*, [Chapter 2: Specification-based testing](https://livebook.manning.com/book/effective-software-testing/chapter-2), sections 2.1–2.4: requirements, partitions, boundaries, and iterative practice. The chapter supports deriving cases from a contract; an ambiguous or incorrect requirement is not repaired by adding tests.
- Aniche, [Chapter 5: Property-based testing](https://livebook.manning.com/book/effective-software-testing/chapter-5), sections 5.1–5.6: example- versus property-based testing and common issues. Properties need deliberate design; generated volume alone is not evidence of correctness.
- Aniche, [Chapter 6: Test doubles and mocks](https://livebook.manning.com/book/effective-software-testing/chapter-6), sections 6.1–6.3: double types, use, and disadvantages. Doubles can isolate behavior but can also hide integration mismatch or couple tests to interactions.
- Aniche, [Chapter 8: Test-driven development](https://livebook.manning.com/book/effective-software-testing/chapter-8), sections 8.3.1–8.3.4, including “when not” and “100% of the time”: TDD is treated as a method with fit conditions, not a universal requirement.
- Google, *Software Engineering at Google* (2020), [Chapter 11: Testing Overview](https://abseil.io/resources/swe-book/html/ch11.html): “Designing a Test Suite,” “Test Scope,” and “A Note on Code Coverage” were reviewed. The chapter says coverage measures execution rather than assertion quality and discusses suite costs and context-dependent composition. Google’s numerical test-mix examples are not prescribed here.
- Google, [Chapter 12: Unit Testing](https://abseil.io/resources/swe-book/html/ch12.html): “Strive for Unchanging Tests,” “Test via Public APIs,” and “Test State, Not Interactions” were reviewed. These are experience-based recommendations from Google's environment, not a universal ban on interaction assertions or test doubles.
- Zeller et al., *The Fuzzing Book*, [Introduction to Software Testing](https://www.fuzzingbook.org/html/Intro_Testing.html), [Reducing Failure-Inducing Inputs](https://www.fuzzingbook.org/html/Reducer.html), and [Mutation Analysis](https://www.fuzzingbook.org/html/MutationAnalysis.html): the testing/checking, reducer, and mutation-analysis material was inspected. The text emphasizes an oracle and reducer predicate; mutation results depend on their assumptions and selected mutants.

Inspection bounds are the actual chapter sections above, as recorded in the chapter review checked 2026-11-21. That date is the research review date, not a publication date. Google chapters are openly accessible, experience-based accounts; their organizational practices and rough ratios are not universal optima. The Fuzzing Book is an online text with its own version history; do not treat the review date as its release date. No causal efficacy claim for testing methods or agent skills follows from these practitioner texts.

## Author advice and synthesis

Contract-derived partitions, boundary analysis, examples, properties, chosen test doubles, and conditional TDD paraphrase Aniche's named chapters. Google chapter advice informs stable behavior-focused boundaries, state assertions, and the distinction between execution coverage and checking behavior. Fuzzing Book material supports meaningful oracles, replayable generated inputs, reduction predicates, and careful interpretation of mutation analysis.

Explicit recommendations to track flaky-test rates statistically, compare conditions, and retain schedule/environment metadata are synthesis extending those sources to nondeterministic concurrent behavior. Statistics may show association or a rate change; they do not establish the causal mechanism by themselves. The balance of isolated and integration tests depends on actual boundary risk, latency, determinism, and project architecture—not a fixed pyramid or ratio.

## Decision examples and evidence checks

1. **Threshold rule with rounding.** For a documented discount at $100, test just below, exactly at, and just above the threshold, then check rounding and exclusions only where specified. Why: partition and boundary cases target likely decision errors without exhaustive values. Verify expected values against an approved contract independent of the implementation.
2. **Mocked adapter but incompatible wire format.** Keep isolated mapping tests and add an integration assertion against the real serializer/schema or service boundary. Why: a mock proves only the mocked interaction contract. Inspect the actual emitted representation and behavior with the dependency that consumers use.
3. **Intermittent parallel failure.** Record outcomes across controlled worker/order/cache conditions and compare failure rates, then inspect a predicted synchronization path. Why: deterministic replay may be unavailable, while statistical comparisons can prioritize hypotheses. Check sample conditions and uncertainty; treat a rate association as a clue until the mechanism or a discriminating experiment supports causality.

The examples are applications, not reported experiments in the cited chapters. Choose verification proportional to the contract and risk; no coverage percentage or test method alone establishes correctness.
