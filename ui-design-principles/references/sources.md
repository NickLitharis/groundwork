# Sources and Scope

This skill is a paraphrase of practitioner interface-design guidance. It is not a book, and no book was inspected for it.

## Inspected sources

- `frontend-design` (Apache License 2.0; the license file is `LICENSE.txt` in that skill's folder). Inspected the full skill text: its opening stance on distinctive design, the subject-first instruction, the typography rules, the list of default treatments that read as generated, the rules on structure and motion, the two-pass plan-then-build process, the restraint and quality-floor section, and the writing section on user-perspective labels, active CTAs, errors, and empty states. This skill paraphrases those ideas in its own wording and does not copy the text. The Apache 2.0 license requires attribution, which this file provides.
- The Apache 2.0 license text was read to confirm that paraphrase with attribution is permitted.

## Book-derived principles

None. The typography rules refer to a style reference (The Elements of Typographic Style) that was not inspected. The skill does not restate its content.

## Not inspected

- The Claude Code design plugin skills (`accessibility-review`, `ux-copy`, `design-critique`, `design-system`, `design-handoff`). Only their descriptions were read. Their principles are not used here. The accessibility-review skill covers WCAG 2.1 AA; a suite skill for accessibility would need its own inspected source.
- Platform guidelines for specific operating systems and frameworks.

## Limits and dated claims

- The specific default treatments named in the source (particular colors and fonts) describe trends at the time of writing. The skill keeps the principle, that a default should be chosen and not inherited, and drops the list of colors.
- Choices of type size, line length, and motion are judgment-based and are not measured results.
- A design that follows these principles may still fail users. User research and testing are separate tasks.

## Modern application

- The quality floor (mobile width, visible focus, reduced motion, readable contrast) applies to any web or native interface. Checking it on the real screen is this skill's application.

## Added after checking against published UI and accessibility sources (read 2026-11-23)

These sources were read and used for the floors, feedback, and error-prevention rules. Each was downloaded and its relevant passages were checked.

- W3C, *Understanding WCAG 2.2*: [Visual Presentation (1.4.8, AAA)](https://www.w3.org/WAI/WCAG22/Understanding/visual-presentation.html): 80-character line length. [Animation from Interactions (2.3.3, AAA)](https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions.html): reduced motion, with `prefers-reduced-motion`. [Focus Visible (2.4.7, AA)](https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html): visible keyboard focus that does not time out. [Contrast (Minimum) (1.4.3, AA)](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html): 4.5:1 for normal text and 3:1 for large text (18 pt, or 14 pt bold). [Use of Color (1.4.1, A)](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html): color is not the only signal. [Target Size (Minimum) (2.5.8, AA)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html): 24×24 CSS pixels, with the 44×44 size as the AAA enhanced target.
- Nielsen Norman Group, [Ten Usability Heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/): heuristic 1, visibility of system status; heuristic 2, match between the system and the real world; heuristic 3, user control and freedom; heuristic 4, consistency and standards; heuristic 5, error prevention; heuristic 8, aesthetic and minimalist design; heuristic 9, recognizing, diagnosing, and recovering from errors.

Not checked: Laws of UX (the index page loaded, but individual laws were not extracted); Norman's and Krug's books (not read for this check). No claim in this skill rests on either.

Levels: the 80-character line length and reduced-motion criterion are AAA. The contrast, focus, and target-size floors are AA. Color-alone is A. The skill labels each level where it cites one.
