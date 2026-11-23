# Sources and Scope

This skill is an original synthesis of the transparency, repair, and maintainability material in the sources below.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt):
  - Chapter 1, "Philosophy": Rule of Transparency, Rule of Repair, and Rule of Robustness, including the Postel passage and the McIlroy response.
  - Chapter 6, "Transparency": "The Zen of Transparency" (abstraction versus visibility), "Designing for Maintainability" (live, dormant, dead code).
  - The section headings of Chapter 6 were reviewed. The case studies (audacity, GCC, kmail, and others) were not inspected, so this skill makes no claim based on them.

## Book-derived principles

- Designing for visibility to make inspection and debugging easier.
- Minimizing unnecessary abstraction over the data being manipulated.
- Failing noisily and as soon as possible when repair is not possible.
- Judging maintainability by whether a community still maintains the code.

## Limits and dated claims

- The chapter's examples are Unix-era programs. The principles are general; the specifics are dated.
- The Postel passage concerns network protocols. The advice to avoid lenient implementations is general.
- The "live, dormant, dead" test is a heuristic. The book offers it without measurement.

## Modern application

- Failure-noise guidance applies to services and libraries alike. Its relation to retries, timeouts, and recovery is covered by the reliability skill.
- Inspectability is applied to logs, traces, and stored state as one design concern. The book does not discuss specific observability products.
