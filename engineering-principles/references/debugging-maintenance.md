# Debugging and Maintenance

Use these examples when a task involves failure diagnosis, repeatable repository commands, generated files, maintainer documentation, or adopting a dependency. They apply the book's ideas to modern coding-agent work; they do not prescribe a particular debugger, build system, document set, or package source.

## Debug from evidence

A report that a request returns an error on a particular input is an observation and a usable reproduction, not a hypothesis about its cause. Preserve those exact conditions. List plausible causes, then choose the smallest inspection or debugger observation that would distinguish them. For example, inspect the parsed value at the boundary before changing validation if the leading hypotheses are malformed input versus a later state transition. Do not ask for redundant reproduction, infer a cause from a symptom, or change several layers at once. Fix the cause, add a regression case, and check the relevant recovery path if the failure can leave state behind. Diagnostics should retain actionable context while excluding credentials and other secrets; silence, fallback values, and broad exception handling must not disguise failure.

The book's transparency discussion links inspectable state and visible failure information to diagnosis and recovery; its runtime-debugging section also values stepping through live state. The modern application here is hypothesis-driven, targeted evidence gathering, including an available debugger—not any specific period tool.

## Repeat the repository's actual workflow

Find the repository's documented setup and existing scripts/configuration before running commands. Record the needed runtime/tool versions, services, environment, fixtures, and any setup steps that are required. Prefer the established build, test, run, and generation entry points used by maintainers and CI. If the test selector reports zero cases or otherwise matches nothing, report that it did not exercise the change; do not present it as passing evidence. Do not add Make or another wrapper solely to standardize commands when the repository already has a workable entry point.

## Keep generated representations aligned

For a generated API client, schema output, lock-derived artifact, or documentation page, locate the source specification and the generator command first. Edit the source of truth, run the existing generation workflow, and inspect both the intended generated diff and surrounding changes. Keep user edits and unrelated generated changes intact. Never patch generated output as the durable fix; a small one-off task does not justify inventing a generator.

This is an application of SPOT and generation: derived copies should follow an authoritative representation. The book advocates generators where they remove real repeated inconsistency, not generation machinery for its own sake.

## Document for the people who need the information

For maintainers, preserve rationale that cannot be recovered from names or current behavior, important invariants, and the main data/control flows. Update the smallest useful set of contributor docs when behavior, setup, or architecture changes. User-facing help should answer the user's task: concise command/API reference for lookup, tutorial steps for learning, and troubleshooting for common failures. Do not create all these forms for a small project or duplicate facts without a reason; link to the authoritative description where possible.

The book distinguishes reference, tutorial, and FAQ by audience. This skill applies that distinction proportionally: choose a useful format and update only affected documentation rather than multiplying documents by rule.

## Evaluate before reusing a dependency

Check whether a candidate solves the actual requirement and whether it is maintained, understandable, documented for its audience, compatible with project versions/platforms, supportable, and acceptable under its license obligations. Compare its integration and build cost, security/operational burden, and future maintenance with implementing and owning the needed capability. Consider existing project dependencies first. Reuse is not automatically cheaper, and building from scratch is not automatically simpler; adopt only when the concrete fit and full-life cost justify it. Do not install a package or rewrite working code merely because reuse is a principle.

The source material identifies quality, documentation, and licensing as reuse concerns. Support, compatibility, operational/build cost, and this comparison are modern decision criteria, not claims quoted from the book.

## Source trail

- Eric S. Raymond, *The Art of Unix Programming*, [full-text PDF](https://cdn.nakamotoinstitute.org/docs/taoup.pdf): chapter 4, “The SPOT Rule” (pp. 115–116); chapter 6, “Transparency, Fault Diagnosis, and Fault Recovery” and “Designing for Maintainability” (pp. 185–186); chapter 15, “Runtime Debugging” (p. 409) and “make: Automating Your Recipes” (pp. 396–397); chapter 16, “Issues in Using Open-Source Software,” especially quality, documentation, and licensing; chapter 18, audience-specific documentation guidance. Exact section titles aid lookup; only page numbers noted in the chapter text are included.
- Chapter 9, “Generation,” especially “Data-Driven Programming” (pp. 249–250), explicitly advises fixing the authoritative specification or translation tool rather than hand-patching generated representations. Apply this through the repository’s existing generator, not an automatic mandate to add one.
