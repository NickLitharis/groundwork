# Complexity

Read this when a change adds or removes a capability, or when a design choice seems simple in one place but may move cost elsewhere. This reference separates the book's framework and examples from this skill's application.

## Where did the work go?

**Book-derived framework.** In *The Art of Unix Programming*, chapter 13, "The Three Sources of Complexity," Raymond distinguishes implementation complexity (how hard the code is to understand and debug), interface complexity (the work users must do), and codebase size. These can move in opposite directions: a terse implementation can force users into repeated low-level work, while a unified mechanism can avoid scattered one-off solutions. "Essential, Optional, and Accidental Complexity" classifies complexity by why it exists: essential complexity is required by the problem; optional complexity buys a capability; accidental complexity is avoidable difficulty in implementing specified behavior.

The editor case study in "A Tale of Five Editors" and "The Right Size for an Editor" contrasts narrow text editing with broader integrated work. The point is not that minimal or expansive editors always win: added capabilities may buy shared context, and must be judged against their objectives and cost. The book's period-specific line-count and defect-density claim is not current empirical evidence.

**Application in this skill.** Trace cost across implementation, interfaces, glue and integration, user effort and error risk, support, and maintenance. Classify proposed work by why it exists. Remove accidental cost; accept optional cost when user value justifies its full-life burden. Treat deadline and time-to-market as inputs to total project effort, not substitutes for it. These are planning heuristics, not empirical claims from the book.
