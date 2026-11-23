# Sources and Scope

This skill is an original synthesis based on the configuration chapter of Raymond's book.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), Chapter 10, "Configuration," [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt). Inspected:
  - "Where Configurations Live": the five-place lookup order and the principle that later, more local settings override earlier ones.
  - "How to Choose among the Methods": matching the mechanism to the expected lifetime of a preference, the batch-versus-interactive distinction, and the advice to provide a command-line option that overrides environment and files.
- Not inspected: "Run-Control Files," the environment-variable and command-line option sections in detail, the portability subsections, "Case Study: fetchmail," and "On Breaking These Rules." This skill does not rely on them.

## Book-derived principles

- Precedence from global to local, with command-line options most local.
- Choose the mechanism by how often a preference changes.
- Provide a command-line override so scripted behavior is well defined.
- Batch tools are configured by options; interactive tools may rely on files.

## Limits and dated claims

- The five-place model is specific to Unix conventions of the 1990s. Current tools use other layouts (for example, XDG directories or application-specific config paths). The principle, not the paths, transfers.
- The book's lookup order is a convention, not a standard. Individual tools may differ; a tool should document its own precedence.

## Modern application

- The lifetime-based placement rule is applied to any settings system, including cloud deployment variables and secret stores.
- The emphasis on fewer settings is a design judgment applied to modern tools. The book does not set a maximum number of options.
