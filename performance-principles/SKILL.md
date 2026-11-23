---
name: performance-principles
description: Use when investigating slow or resource-heavy software, setting performance objectives, comparing implementations, or deciding whether optimization is worthwhile. Workload-based and correctness-preserving. Not a tuning recipe.
---

# Improve performance with evidence

Optimize an outcome that matters, not a number detached from workload. Performance work is an engineering tradeoff, not a mandatory phase after every change. Keep the ordinary implementation clear until a real constraint, target, or likely scaling problem justifies deeper measurement.

## Define the workload and objective

Describe the operation, representative input shape and distribution, arrival rate or concurrency, warm/cold state, and relevant environment. Include the runtime and build mode where they affect execution (for example, JIT warm-up, garbage collection, or interpreter/compiler settings), and deployment limits that constrain resources (such as container CPU or memory quotas). Name the user or system outcome and metric: p95 interactive latency, batch completion time, useful jobs/s at stated concurrency, peak resident memory, or bytes/item. State the baseline, target or comparison, acceptance conditions, and correctness constraints. A small number of meaningful objectives is usually clearer than a dashboard of proxies.

Avoid optimizing a proxy just because it is easy to collect. A service's user-visible latency can differ from server processing time; a high batch rate does not establish quick individual responses.

## Find the limiting cost

Establish a representative baseline, then use profiling, tracing, counters, or controlled experiments to locate the dominant cost. Follow evidence across CPU, allocation/garbage collection, memory capacity and locality, synchronization, storage, network, and queueing. In managed runtimes, distinguish startup/interpreter behavior from warmed JIT code and account for collection pauses or allocation pressure when they occur; do not assume either is important without evidence. A high utilization reading alone does not prove a bottleneck: look for saturation, waiting, or a change in the target outcome. Profilers and instrumentation perturb behavior, so use them to find causes and confirm important findings with an outcome measurement under the intended runtime and load.

Check algorithmic growth across the input sizes and distributions the contract includes. A better asymptotic bound can matter at scale, but fixed costs, data layout, cache behavior, memory pressure, and access patterns affect practical crossover points. Likewise, adding parallelism can improve throughput only when useful work exceeds coordination, contention, and resource costs; more workers may worsen latency under a CPU quota or shared load. Test the relevant regime rather than treating a complexity label or machine-core count as a performance result.

## Make the smallest useful change

Change the demonstrated cause, preserve the behavior contract, and compare against the same workload. Consider end-to-end cost: allocation and copying, memory footprint and locality, I/O and round trips, batching, concurrency, and cache/coherency overhead. Batching may increase throughput while raising per-item latency or memory use. Caching may reduce repeated work while adding invalidation, freshness, memory, and synchronization costs. Prefer reducing unnecessary work or a demonstrated scaling problem over clever low-level tuning without evidence.

Retest correctness and relevant edge cases as well as performance. A faster result that omits work, changes outputs, hides errors, or uses unrealistic assumptions is not an improvement.

## Decide whether to stop

Report workload and environment, metric and units, baseline and candidate, measurement boundary, method and repetitions, distribution or variability, correctness evidence, and relevant resource tradeoffs. For latency-sensitive work, report a meaningful tail percentile as well as typical behavior; for throughput, state concurrency and pair rate with latency/resource use when queueing or saturation may change the result. Treat differences within measurement noise as inconclusive. Keep a change when it meets the objective or shows a meaningful, repeatable benefit that justifies its complexity and operating cost. Stop when the objective is met, the remaining bottleneck is outside scope, or credible gains no longer justify added risk or maintenance. Record uncertainty instead of claiming a win.

For worked examples and noise controls, read [Measurement and tradeoffs](references/measurement-and-tradeoffs.md) as needed. Reliability skills cover overload, deadlines, retries, and recovery when failure behavior is the main concern; this skill addresses measured performance and does not require a reliability workflow for every optimization.