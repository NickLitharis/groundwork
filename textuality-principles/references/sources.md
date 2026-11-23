# Sources and Scope

This skill is an original synthesis based on the textuality chapter of Raymond's book. Quotations are not reproduced.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), Chapter 5, "Textuality," [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt). Inspected "The Importance of Being Textual," including the passage on binary formats and the anecdote about a binary device file replaced by text. The section headings for metaformats, the Unix text conventions, and application protocol metaformats were reviewed as headings only. Their bodies were not inspected, so this skill makes no claim about specific formats.

## Book-derived principles

- Text streams are a universal, transparent interchange format.
- Text's limitations help enforce encapsulation.
- A complex binary design calls for a deliberate check: measure first, and consider text with compression.

## Limits and dated claims

- The chapter's examples are Unix-era file and protocol formats. Their details are dated.
- The chapter does not cover modern serialization formats in depth. Choices among them are application decisions.
- The book's claims about binary speed reflect the hardware and I/O conditions of the time. Measure in the target environment.

## Modern application

- The skill applies to logs, configuration, API payloads, and stored data alike.
- Delimiter and escaping advice is an application of general format-design practice, not a claim from the chapter.
