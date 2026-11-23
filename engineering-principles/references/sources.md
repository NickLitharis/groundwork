# Sources and Scope

This skill is an original synthesis of engineering principles and practical agent guidance. Links identify inspiration and further reading, not runtime dependencies. No external skill needs to be installed, and the agent does not need to fetch these pages to apply this skill.

## Primary Unix material

- Eric S. Raymond, *The Art of Unix Programming*, [Basics of the Unix Philosophy](https://cscie2x.dce.harvard.edu/hw/ch01s06.html): modularity, clarity, composition, separation, simplicity, transparency, representation, least surprise, silence, repair, economy, generation, optimization, diversity, and extensibility. Includes Doug McIlroy's formulation and Rob Pike's programming rules. Apply these as pragmatic guidance, not a mandate for text-only protocols or one universal architecture.
- Eric S. Raymond, *The Art of Unix Programming*, [full-text PDF](https://cdn.nakamotoinstitute.org/docs/taoup.pdf): chapter 11, “Interfaces” (pp. 289–326), especially “Evaluating Interface Designs,” “Tradeoffs between CLI and Visual Interfaces,” “The Filter Pattern,” and “The Separated Engine and Interface Pattern”; chapter 12, “Optimization” (pp. 327–334), especially “Measure before Optimizing,” “Throughput vs. Latency,” and “Caching Operation Results”; chapter 13, “Complexity” (pp. 335–358), especially “The Three Sources of Complexity,” “Essential, Optional, and Accidental Complexity,” and “The Right Size of Software.” These chapters inform the distinctions and examples in [Complexity](complexity.md). The skill’s whole-life cost and stop-criterion guidance is an original planning application; the book’s historical measurements and hardware comparisons are not treated as current empirical evidence.
- Eric S. Raymond, *The Art of Unix Programming*, [full-text PDF](https://cdn.nakamotoinstitute.org/docs/taoup.pdf): chapter 4, “The SPOT Rule” (pp. 115–116); chapter 6, “Transparency, Fault Diagnosis, and Fault Recovery” and “Designing for Maintainability” (pp. 185–186); chapter 15, “Runtime Debugging” (p. 409) and “make: Automating Your Recipes” (pp. 396–397); chapter 16, “Issues in Using Open-Source Software”; chapter 18, audience-specific documentation. These inform repository-workflow and dependency practices in this skill's main text, not a mandate to use Make, historical debugger tools, a fixed documentation set, or the book's period-specific claims.

- Martin Fowler, [YAGNI](https://martinfowler.com/bliki/Yagni.html): avoid presumptive functionality; this is not an excuse to neglect code health.

## Agent-skill inspiration

- [engineering-principles — manojbajaj95/skills](https://www.skills.sh/manojbajaj95/skills/engineering-principles): YAGNI, deep modules, trusted libraries, separation of concerns.
- [unix-philosophy — lilucpp/code-craft](https://github.com/lilucpp/code-craft/blob/HEAD/.agents/skills/unix-philosophy/SKILL.md): composable interfaces, policy/mechanism separation, CLI streams. This synthesis deliberately omits fixed API-concept quotas and mandatory configuration hierarchies.
- [software-engineering — BejeweledMe/codex-pro-agent-skills](https://github.com/BejeweledMe/codex-pro-agent-skills/blob/main/skills/software-engineering/SKILL.md): maintenance over time, risk-proportionate changes, behavior-focused tests, compatibility and migrations.
- [clean-code — cskwork/clean-code](https://www.skills.sh/cskwork/clean-code/clean-code): focused refactoring, characterization tests, preservation of observable contracts.

## Deliberate boundaries

Language-agnostic and tool-agnostic. No mandatory framework, object-oriented design, dependency, test runner, coverage percentage, numeric code-size limit, multi-agent workflow, or report template. Repository-specific requirements and specialized language/security guidance still apply. This skill supplies engineering judgment, not a replacement for them.

For chapter-grounded design, complexity, interface, performance, and test tradeoffs—plus inspected-content limits and realistic decision examples—see [Chapter foundations](chapter-foundations.md). Farley’s preface and Chapter 3 are the only inspected portions of *Modern Software Engineering*; no detailed claims are drawn from its unread design chapters.
