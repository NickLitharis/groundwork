# Complexity and performance

## Complexity and interfaces

*The Art of Unix Programming*, ch. 13: “The Three Sources of Complexity” (pp. 335–337), “Tradeoffs between Interface and Implementation Complexity” (pp. 337–339), “Essential, Optional, and Accidental Complexity” (pp. 339–340), “Mapping Complexity” (pp. 340–342), “When Simplicity Is Not Enough” (pp. 342–343), and “The Right Size of Software” (pp. 357–358). Synthesis: distinguish agreed behavior, selected feature cost, and avoidable implementation complexity. Complexity shifted to user effort, operations, or shared context still counts. A batch operation may add implementation work yet remove repetitive steps; retain it if part of the agreed outcome.

Chapter 11: “Evaluating Interface Designs” (pp. 293–295), “Tradeoffs between CLI and Visual Interfaces” (pp. 295–298), and “Case Study: Two Ways to Write a Calculator Program” (pp. 298–300). Match interfaces to users, task frequency and scale, visual feedback, and automation. A one-off image edit and repeated bulk transformation have different interaction costs.

## Performance

Chapter 12: “Measure before Optimizing” (pp. 328–330), “Throughput vs. Latency” (pp. 331–332), and “Caching Operation Results” (pp. 333–334). Benchmark representative workload and metric; feasibility is not performance evidence. Caching may reduce latency but adds consistency and recovery cost.
