# Sources and Scope

This skill is an original synthesis based on the opening of the portability chapter of Raymond's book. The chapter's remaining sections were not inspected.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), Chapter 17, "Portability," [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt). Inspected the chapter opening and the section "Software Portability and Keeping Up Standards" (the operating system as the stable layer, avoidance of hardware dependencies beyond the C abstract machine, the preference for open standards, and the observation about throwaway code persisting).
- Not inspected: the rest of Chapter 17, including its later sections on standards and the portability of specific tools and languages.

## Book-derived principles

- Write to the stable interface, not to hardware details.
- Prefer open standards to perishable technologies.
- Expect small tools to outlive their plans.
- Keep platform dependence in a small, explicit place.

## Limits and dated claims

- The chapter is grounded in Unix portability between processor families of the 1970s and later. The historical examples are dated.
- The claim that hardware-dependent code is "bad form" reflects the C-era view. Modern systems have many platform-specific paths that are not kernel code; this skill applies the principle to isolation, not to prohibition.
- The chapter does not address modern container, cloud, or runtime-version portability. Those are application decisions.

## Modern application

- Isolating platform code behind a named boundary is an application of the chapter's principle to modern build and deployment targets.
