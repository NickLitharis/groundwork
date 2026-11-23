# Sources and Scope

This skill is an original synthesis. It applies the Unix design rules as tests and does not reproduce the book's text.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), Chapter 1, "Philosophy," [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt). Inspected the 17-rule list and the discussions of the Rule of Modularity, Clarity, Parsimony, Silence, Repair, Economy, and Optimization, plus the rule summaries that introduce them. Passages on Rule of Composition, Separation, Simplicity, Transparency, Representation, Least Surprise, Generation, Diversity, and Extensibility were read at the summary level only.

## Book-derived principles

- Rules as a compact design vocabulary, with tradeoff-driven application.
- Controlling complexity through simple parts and well-defined interfaces.
- Prototype before optimizing; avoid building large programs before the need is demonstrated.

## Limits and dated claims

- The rules were written for small Unix tools. Their stated motivations include slow printing terminals and the economics of 1970s-era machines. These motivations are historical.
- The book's own rule list is not presented as complete or universal. The book warns against "one true way" thinking, and this skill follows that caution.
- The book does not address service deployment, distributed systems, or agent-based tooling. Applying the rules to those contexts is this skill's adaptation.

## Modern application

- The rules are applied as questions to answer during design, not as a checklist.
- Deployment choices (monoliths, services, functions) are outside the rules' scope and are decided on other grounds.
