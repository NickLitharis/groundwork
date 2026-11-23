# Source Registry

Registry for the research collection plan behind the Groundwork suite. Verification dates: 2026-11-23.

Two kinds of verification are recorded. **HTTP** means the URL returned a status code to curl; the content was not read. **Read** means the text was downloaded and inspected for this registry. Search results are not treated as verification.

## Registry

| # | Source | Access URL | Access status | Skills fed | Required sections | Verification note |
|---|---|---|---|---|---|---|
| 1 | Raymond, *The Art of Unix Programming* (2003) | https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt | Full text (plain text) | unix-philosophy, modularity, textuality, transparency, composition, minilanguage-generation, configuration, interface, performance, complexity, documentation, portability, communication, evolution | Ch. 1 Philosophy; Ch. 4 Modularity; Ch. 5 Textuality; Ch. 6 Transparency; Ch. 7 Multiprogramming; Ch. 8 Minilanguages; Ch. 9 Generation; Ch. 10 Configuration; Ch. 11 Interfaces; Ch. 12 Optimization; Ch. 13 Complexity; Ch. 16 Reuse; Ch. 17 Portability; Ch. 18 Documentation | Read 2026-11-23. Chapter numbers corrected against the TOC; earlier numbers were wrong from Ch. 4 onward. Chapter 11 and the rule list were read; not all sections were read. |
| 2 | Kernighan & Pike, *The Practice of Programming* (1999) | https://archive.org/details/the-practice-of-programming | Full text on archive.org, open-source collection, no lending restriction; plain text not read | unix-philosophy, testing, debugging, performance, portability, interface | Style; Design and Implementation; Testing and Debugging; Performance; Portability; Interfaces | Metadata read 2026-11-23. Not used for any claim yet. Chapter list is from memory and unverified. |
| 3 | Kernighan & Pike, *The Unix Programming Environment* (1984) | https://archive.org/stream/UNIXProgrammingEnvironment/UnixProgrammingEnvironment_djvu.txt | Full text (plain text) | composition, textuality, debugging | Ch. 2 File System; Ch. 3 Using the Shell; Ch. 4 Filters; Ch. 5 Shell Programming; Ch. 7 System Calls; Ch. 8 Program Development; Ch. 9 Document Preparation | Contents read 2026-11-23. Ch. 6 title not confirmed. Body text not used. |
| 4 | Ousterhout, *A Philosophy of Software Design* (2018) | https://archive.org/details/a-philosophy-of-software-design_202503 | Full text on archive.org, open-source collection, no lending restriction; OCR is poor in places | modularity, complexity, evolution, communication | Ch. 4 Modules Should Be Deep; information hiding; complexity chapters | Metadata read 2026-11-23. Ch. 4 read; deep-module definition confirmed. Other chapters not read. |
| 5 | Brooks, *The Mythical Man-Month* (1975; 1995 anniv. ed.) | https://dl.acm.org/doi/book/10.5555/207583 | **Blocked**: HTTP 403. Treat as print-only unless library or ACM access is available. | complexity, evolution | Second-system effect; surgical team; conceptual integrity | HTTP 403 on 2026-11-23. Not read. |
| 6 | Raymond, *The Cathedral and the Bazaar* (1999) | http://www.catb.org/~esr/writings/cathedral-bazaar/ | Online HTML | evolution, reuse | Named principles | HTTP 200 on 2026-11-23. Not read. |
| 7 | Bhatti et al., *Docs for Developers* (2021) | https://link.springer.com/book/10.1007/978-1-4842-7217-6 | Publisher page; preview expected | documentation | Documentation as product; information architecture | HTTP 200 on 2026-11-23. Preview not read. |
| 8 | Gentle, *Docs Like Code* | https://www.docslikecode.com/book/ | Free online | documentation | Workflow chapters | HTTP 200 on 2026-11-23. Not read. |
| 9 | Procida, Diátaxis framework | https://diataxis.fr/ | Free online | documentation | Four needs: tutorial, how-to, reference, explanation | HTTP 200 and homepage read 2026-11-23. Full site not read. |
| 10 | Fowler, *Domain-Specific Languages* (Addison-Wesley, 2010) | https://books.google.com/books?id=ri1UpCG2C5IC | **Broken**: HTTP 404. Print ISBN 9780321712943; another listing shows 9780132107549. Find a working Google Books link by ISBN. | minilanguage-generation | Internal vs. external DSLs | HTTP 404 on 2026-11-23. A search found publisher listings but no Google Books entry. Not read. |
| 11 | Lauret, *The Design of Web APIs* (Manning) | https://www.manning.com/books/the-design-of-web-apis | Publisher page; free preview chapters exist (the preview found was for the second edition) | interface (web APIs out of current scope) | Design guidelines; naming; errors | HTTP 200 on 2026-11-23. Preview for the first edition not confirmed. Not read. |
| 12 | Palos, *Designing APIs Humans Love* | https://play.google.com/store/books/details?id=Q0j0EQAAQBAJ | **Unverified**: link returns HTTP 200, but search found no matching book or author. The nearest match is Jin et al., *Designing Web APIs* (O'Reilly, 2018). | interface (if used) | Unknown | Confirm title and author with the owner before citing. Not read. |

## Corrections to the earlier plan

- Chapter numbers in TAOUP were wrong from Ch. 4 onward. Corrected above.
- The Fowler link in the plan returned 404.
- The Palos title and author in the plan could not be found.
- The ACM link returns 403.
- Search queries do not verify links. Only the HTTP checks and the reads recorded above count.

## Summary by verification level

- **Read:** TAOUP (chapters 1, 4–11, 17–18 in part), UPE (contents), APoSD (chapter 4), Diátaxis (homepage), PoP (metadata only).
- **HTTP only:** Cathedral and Bazaar, Docs for Developers, Docs Like Code, Manning Design of Web APIs, Palos.
- **Blocked or broken:** Mythical Man-Month (403), Fowler DSL Google Books (404), Palos title (unconfirmed).
