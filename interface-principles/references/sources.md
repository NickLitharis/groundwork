# Sources and Scope

This skill is an original synthesis based on the interface chapter and related material in Raymond's book. Its scope is general interface principles. HTTP and REST API design are not covered, and no API source was inspected for this skill.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt):
  - Chapter 11, "Interfaces," "Applying the Rule of Least Surprise": the rationale based on limited attention, the warning against novelty, the caution against mechanical conservatism, and delegation to familiar programs.
  - Chapter 11, "Silence Is Golden": standard error for real errors, standard output free of unrequested data, and the guidance that progress indicators are acceptable while unnecessary confirmation dialogs are not.
  - Chapter 1, "Philosophy": Rule of Least Surprise and Rule of Silence, including the Ken Arnold note on attention.
- Not inspected: "History of Interface Design on Unix," "Evaluating Interface Designs," "Tradeoffs between CLI and Visual Interfaces," "Case Study: Two Ways to Write a Calculator Program," and the interface pattern sections (Filter, Cantrip, Source, Sink, Compiler, ed, Roguelike, CLI Server, Language-Based, Polyvalent-Program, Web Browser). They appear in the table of contents and are not distilled here.
- Chapter 4, "Modularity" was used for the test that an interface should be describable in plain language. That passage is cited in the modularity skill and is referenced here only for the interface-description habit.

  - Chapter 1, "Philosophy": the Postel passage and the McIlroy response, cited for the rule that specifications should be generous and implementations should not silently accept malformed input.
- `references/cli-contracts.md` is a modern-practice synthesis of stream, exit-status, and option conventions. It was moved here from the engineering skill. The conventions are not claims inspected in the book; the book supports only the Unix stream and silence principles above.

## Book-derived principles

- Least surprise, grounded in the limits of human attention.
- Standard output for data; standard error for real errors; no unrequested output.
- Delegate interface functions to user-chosen tools where practical.
- Describe an interface in plain language before implementing it.

## Limits and dated claims

- The book's examples are command-line tools on Unix. Their specific conventions (for example, terminal width or line-based output) are dated.
- The book does not address web APIs, SDKs, or language-level public APIs in depth. Those claims need separate sources.
- Its guidance on GUI popups reflects the desktop era. The principle, not the specific advice, applies to modern interfaces.

## Modern application

- The stdout and stderr separation applies to any CLI intended for scripting.
- The non-interactive path rule is an application of the book's scriptability guidance to modern tools.
