# Sources and Scope

This skill is an original synthesis based on the minilanguage and generation chapters of Raymond's book. It does not reproduce the case studies.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt):
  - Chapter 8, "Minilanguages," section "Choosing the Right Complexity Level": simplicity first, structured data over a language that modifies external data, and the warning about embedded languages in networked contexts.
  - Chapter 8, "Designing Minilanguages": the condition under which a minilanguage is appropriate (simple, stereotyped primitives with varied use).
  - Chapter 9, "Generation," "Data-Driven Programming": separating code from data, and pushing changes upstream rather than hacking generated output.
  - Chapter 9, "Ad-hoc Code Generation": introductory material only.
  - Chapter 1, "Philosophy": Rule of Generation.
- Not inspected: the case studies in Chapter 8 (regular expressions, XSLT, Emacs Lisp, JavaScript, and others) and the taxonomy diagram. This skill does not rely on their specifics.

## Book-derived principles

- Prefer structured data over a minilanguage where possible.
- A minilanguage is appropriate for simple, stereotyped primitives with fluid use.
- Embedded programmability has security costs.
- Data-driven design: the program's behavior changes by editing data.
- Push problems upstream; do not hand-edit generated output.

## Limits and dated claims

- The security examples (JavaScript pop-ups and macro malware) are from the book's era. The principle transfers; the specific incidents do not.
- The book does not evaluate modern DSL frameworks or parser generators.
- Fowler's *Domain-Specific Languages* is listed in the project's source plan but was not inspected for this skill. Its taxonomy of internal and external DSLs is not used here.

## Modern application

- Generated-code traceability and data-driven design apply to build pipelines, schema generators, and configuration templates alike.
