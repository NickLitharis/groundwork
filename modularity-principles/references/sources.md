# Sources and Scope

This skill is an original synthesis of the modularity material in the sources below. Passages were read from the full texts; quotations are not reproduced.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), Chapter 4, "Modularity," [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt). Inspected "Encapsulation and Optimal Module Size" (encapsulation, APIs as choke points, the plain-language test for an API, module size and the cited defect-density study), "The Value of Detachment," and "Glue Layers" (thin glue, impedance matching between layers).
- John Ousterhout, *A Philosophy of Software Design* (2018), Chapter 4, "Modules Should Be Deep," [full text, archive.org](https://archive.org/details/a-philosophy-of-software-design_202503). Inspected the deep-module definition (benefit as functionality, cost as interface), the example of the Unix file I/O interface, and the information-hiding section. The archive's OCR text is poor in places; the claims here are paraphrased from the surrounding passages.

## Book-derived principles

- Encapsulation through narrow APIs; interfaces define the architecture.
- Writing an informal description of an interface before implementing it.
- Depth: the value of a module relative to its interface cost.
- Information hiding: design decisions stay out of interfaces.
- Glue layers should be thin.

## Limits and dated claims

- Raymond's module-size point rests on a cited study of defect density (Hatton, 1997). This skill cites the study as a caution only. It does not prescribe a size.
- The Unix I/O example is a 1970s design. The principle transfers; the specific calls do not.
- Both sources emphasize design judgment over measurement. Ousterhout's depth metric is a qualitative test, not a formula.

## Modern application

- Module boundaries are applied to services, libraries, and in-process components alike.
- Module depth is judged by reviewing the interface and what it hides, not by counting lines or classes.
