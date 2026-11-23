# Sources and Scope

This skill is an original synthesis based on the documentation framework below and on the documentation discussion in Raymond's book.

## Inspected sources

- Daniele Procida, Diátaxis framework, [diataxis.fr](https://diataxis.fr/). Inspected the site's statement of the four needs (tutorials, how-to guides, reference, explanation) and the organizing principle. The full site contains more material; only the opening framework was reviewed for this skill.
- Eric S. Raymond, *The Art of Unix Programming* (2003), [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt):
  - Chapter 18, "Documentation," opening and "Documentation Concepts": the distinction between WYSIWYG tools and markup-centered tools, and the observation that man pages remained the most important form of Unix documentation.
  - Chapter 4, "Modularity," "Encapsulation and Optimal Module Size": writing an informal description of an interface before coding it.

## Book-derived principles

- Documentation should be organized by the reader's need.
- Describe interfaces in plain language before implementing them.
- Reference documentation for each interface is a required deliverable.

## Limits and dated claims

- The book's documentation chapter covers format toolchains of the 1990s and early 2000s. Those toolchain details are dated and not used here.
- Diátaxis is a framework, not a measured result. This skill applies its four-part classification as a working model.
- *Docs for Developers* (Bhatti et al.) and Anne Gentle's *Docs Like Code* were not inspected for this skill. They are not cited for any claim.

## Modern application

- The four-part classification applies to any documentation set: product docs, library references, internal runbooks.
- Keeping docs close to code and updating them with the change is an application of general docs-as-code practice, not a claim from any source inspected here.

## Migrated from practitioner skills (not books)

- "Write explanations that show the mechanism" was extracted from a local explanation procedure (`ds-explain`). Inspected: its steps (size the reader's need, trace the runtime path, separate the record from inference, cite file and line) and rules (no guesses presented as fact, explain ideas rather than list functions).
- "Write agent-facing project docs" was extracted from a local CLAUDE.md audit procedure (`claude-md-improver`). Inspected: its discovery and quality criteria (commands and workflows, architecture clarity, non-obvious patterns, conciseness, currency, actionability) and its rule to propose minimal, targeted additions. Its numeric scoring weights are not used here.

## Scope note (moved from SKILL.md)

The book's documentation chapter discusses formatting toolchains (troff, markup, and WYSIWYG tools) and their history. Those details are dated and are not distilled here. The current docs-as-code practice (Gentle, *Docs Like Code*; *Docs for Developers*) was not inspected for this skill and is not cited for specific claims.
