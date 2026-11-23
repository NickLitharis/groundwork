---
name: textuality-principles
description: Use when designing a file format, a wire protocol, a record or log format, or any data that programs or people exchange; deciding between text and binary; or reviewing a format for transparency and encapsulation. Favors human-readable representations unless a measured need justifies otherwise. Not a guide to any particular serialization library.
---

# Make data formats readable first

A data format is an interface that outlives its first implementation. Start with a representation that a person can read, edit with ordinary tools, and inspect when something goes wrong. Move away from text only when a measured need demands it.

## Default to text for interchange

Text streams are easy for people to read, write, and edit without special tools. Format designs can usually be made transparent in this way. Choose text as the default for configuration, logs, and interchange between programs, and document any fields that a person may need to edit by hand.

## Let limited formats enforce boundaries

Text formats discourage elaborate, densely encoded structure. That limitation helps encapsulation: a program is less likely to expose its internal state to another program when the format cannot carry it easily. Treat a format's limits as a feature when they keep components apart.

## Pause before designing a binary format

A complex binary format or protocol is a strong signal to stop and reconsider. Before committing to binary for speed, measure the text version. If size is the concern, compression on a text stream is often a cleaner answer than a binary layout. The book's anecdote of a binary device file that was replaced by plain text, with negligible speed penalty, is one example of this trade-off.

## Keep the format's own rules consistent

Use one convention for delimiters, escaping, comments, and versioning across a format family. The book catalogs many file metaformats, including delimiter-separated, record-based, and key-value styles. This skill does not endorse any one of them; choose the simplest that the data needs and document its rules.

## Watch for these failure modes

- Binary formats chosen for speed without a measurement.
- Text formats with undocumented delimiters or escape rules, which break when data contains the delimiter.
- Format changes that are not versioned, leaving readers unable to distinguish old and new data.
- Formats that carry internal implementation details that callers then depend on.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [transparency](../transparency-principles/SKILL.md) for inspectability, [composition](../composition-principles/SKILL.md) for how formats move between programs, [evolution](../evolution-principles/SKILL.md) for changing a stored format.
