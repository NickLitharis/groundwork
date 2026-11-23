# Sources and evidence boundaries

This reference records the material inspected for `evolution-principles`. Recommendations distinguish author advice, current operational documentation, and synthesis. The source review does not establish that this skill improves agent performance.

## Inspected sources

- Martin Fowler, *Refactoring: Improving the Design of Existing Code*, 2nd ed. (2018), Chapter 1, “Refactoring: A First Example.” The actual chapter text was inspected in the freely distributed Thoughtworks sample PDF. It demonstrates self-checking behavior comparisons, small transformations, checks after each step, and refactoring to make a needed behavior change easier. It also says not to refactor code that will never change and creates no comprehension burden. This is chapter 1 only, not the whole book or proof that unit tests protect external contracts. [Chapter 1 PDF](https://www.thoughtworks.com/content/dam/thoughtworks/documents/books/bk_Refactoring2-free-chapter_en.pdf); [edition history](https://martinfowler.com/articles/refactoring-2nd-ed.html).
- Kent Beck, *Tidy First?* (O’Reilly, 2023), publisher contents and a brief accessible opening of the author essay “First, After, Later, Never.” The contents list timing/batch-size topics; the prose beyond the free opening was unavailable. No detailed rule here is attributed to unread book chapters. [Publisher listing and contents](https://www.oreilly.com/library/view/tidy-first/9781098151232); [author essay](https://kentbeck.com/2022/07/29/first-after-later-never/).
- GitLab, “Backwards compatibility across updates.” Current engineering guidance describes non-atomic deployments, mixed web/API/worker/database versions, and queued work crossing version boundaries. It uses expand → migrate → contract as a pattern and notes that flags are not themselves a compatibility strategy. This is a GitLab operational example, not a universal schedule. [Guide](https://docs.gitlab.com/development/multi_version_compatibility/).
- GitLab, “Avoiding downtime in migrations.” The inspected guide explains that destructive schema changes, such as dropping columns, are difficult to roll back and illustrates staged removal and background migration. Apply the mechanism only where data volume and deployment model call for it. [Guide](https://docs.gitlab.com/development/database/avoiding_downtime_in_migrations/).
- Fowler, “Refactoring Malapropism.” The author distinguishes behavior-preserving refactoring from broader restructuring and notes that the former presumes defined behavior. This supports naming the boundary and intent rather than using “refactor” for every change. [Article](https://martinfowler.com/bliki/RefactoringMalapropism.html).
- Ayas, Leitner, and Hebig (2023), empirical study of microservice migrations, based on 19 practitioner interviews across 16 companies and qualitative analysis of public Q&A. It reports long-running, iterative organizational and technical work; it is not a causal comparison showing microservices outperform another architecture. [Open-access study](https://pmc.ncbi.nlm.nih.gov/articles/PMC10201508/).

## Synthesis and limits

Fowler's behavior-preserving local transformations do not by themselves prove API, schema, event, or mixed-version compatibility. GitLab's deployment guidance supplies concrete examples of consumers coexisting across versions. The recommendation to test intermediate states and delayed work is a synthesis from those deployment conditions, not a claim that every project needs a multi-release migration.

A destructive data change can make binary rollback insufficient. Planning restore, reverse migration, reconciliation, compensation, or roll-forward follows from the documented difficulty of reversing destructive changes; which recovery is valid is system-specific. External effects are not assumed reversible. No compulsory shim or three-release protocol follows from these sources.

*Designing Data-Intensive Applications*, 2nd ed. publication was confirmed, but publisher chapter prose was inaccessible; no principle here is attributed to its chapters. *Tidy First?* beyond its contents and accessible essay opening was not inspected. No chapter claims from either are made.

## Decision examples: why and how to check

1. **A private refactor precedes a feature.** Why: a known upcoming behavior change is awkward, while a structural step can retain observable behavior. How to check: establish a relevant characterization first, make local changes, rerun it; separately verify the feature's contract. Do not infer unobserved external behavior from that characterization.
2. **A nullable database field is being removed under rolling deployment.** Why: old code and delayed jobs may continue to depend on it. How to check: map deployed readers/writers and message retention, test intermediate schema/version combinations, observe that old use ended, and only then remove it. Choose a recovery path before destructive contraction.
3. **A partner API changes its response shape.** Why: consumers outside the deployer's atomic rollout make this an intentional contract change. How to check: use consumer evidence or an agreed compatibility window, test old and new shapes through the transition, and document whether recovery requires restore or a forward fix. Do not assume a released response can be recalled.

## Migrated from a practitioner skill (not a book)

The section "Find what a change breaks outside its diff" and its five-level proof grading were extracted from a local practitioner procedure (`ds-blast-radius`). Inspected: its steps (find the facts the change is safe because of; look where search stops; grade each key fact; push cheap facts to a runnable check; report with output) and its rule that a write-up is not proof. No book was inspected for this section.
