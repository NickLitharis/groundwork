# Planning evidence and project practices

Use this reference only when the task involves debugging, project workflow, generated representations, maintainer-facing information, or adopting reusable software. These are planning questions—not a required checklist or an implementation recipe. Scale investigation to impact, reversibility, and uncertainty. A request for a plan still does not authorize implementation.

## Bugs: evidence and recovery

Before committing to a fix, bound investigation by a concrete question and a stopping point. Record what is observed, plausible hypotheses, and the evidence that would confirm or reject each. For example, for an intermittent failed import, first compare a failing input and a successful one, then decide whether the evidence points to parsing, environment, or ordering; do not promise a parser rewrite before that decision. Acceptance can include reproducing the failure, confirming the diagnosis, verifying the fix, and checking that operators can identify and recover from the relevant failure state. Plan only diagnostics or recovery behavior the real risk needs.

## Repeatable project tooling

Inspect the repository’s declared commands, setup notes, CI configuration, and required services before ordering implementation and verification. Plan to use the project’s established build, test, generation, and validation paths, including their prerequisites. If a meaningful check is absent, inaccessible, or too costly, state the limitation and choose narrower evidence proportionate to the risk; do not fabricate a command or equate “no check available” with “verified.” Reuse existing CI checks instead of implementing equivalent parallel checks; their existence is not evidence that they passed for this change.

## Authoritative sources and generated artifacts

Identify where each important fact is authoritative: for example, a schema, configuration source, API definition, or data table. Trace any generated output to its source and generator, discover consumers, prerequisites, and ordering constraints, and plan checks for both generated consistency and affected consumers. If an API schema generates client bindings consumed by a service, update the schema and regenerate before testing that service—not an independently edited generated copy. Generation is useful when it keeps representations aligned; it does not justify introducing a generator or a higher-level specification without a present need.

## Maintainer information by audience

Ask which people need to understand, operate, extend, or troubleshoot this change. Include rationale, a short onboarding note, or a troubleshooting detail when it closes a real knowledge gap for those maintainers. Update existing project guidance where that is enough; do not add a handbook, FAQ, or documentation pipeline by default. For example, a non-obvious migration order may warrant a maintainer note, while an easily understood local refactor may need no new documentation.

## Reuse candidates

First look for a suitable capability already in the project. If an external package or tool is a credible option, compare its fit to the actual requirement, usable documentation, license obligations, maintenance/support signals, integration and update cost, and the cost of later removal or replacement. A small comparison of two realistic candidates may resolve a consequential choice; exhaustive market research does not. Do not treat popularity or availability as proof of fit, and do not install or procure a candidate merely because planning considered it. Refer legal questions to the appropriate reviewer rather than inferring obligations from historical summaries.

## Source and scope

This guidance adapts ideas from *The Art of Unix Programming* by Eric S. Raymond (2003), especially chapter 4, “Modularity” (SPOT and authoritative representations); chapter 6, “Transparency” (diagnosis, recovery, and maintainability); chapters 8–9, “Minilanguages” and “Generation” (declarative specifications and derived outputs); chapter 15, “Tools” (build recipes and runtime debugging); chapter 16, “Reuse” (quality, documentation, and license considerations); and chapter 18, “Documentation” (distinct reader audiences). [Source PDF](https://cdn.nakamotoinstitute.org/docs/taoup.pdf).

The book’s Unix examples motivate these questions, not a mandate to adopt its tools or historical claims. Its empirical generalizations, tool recommendations, and legal discussion are not treated here as current evidence or legal advice. The modern application is to plan evidence, sequencing, verification, and ownership using the actual project and its users.
