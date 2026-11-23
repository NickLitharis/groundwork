# Sources and Scope

This skill is an original synthesis based on the multiprogramming chapter of Raymond's book. The chapter's taxonomy is reorganized here by coupling rather than reproduced.

## Inspected sources

- Eric S. Raymond, *The Art of Unix Programming* (2003), Chapter 7, "Multiprogramming," [full text, archive.org](https://archive.org/stream/ost-computer-science-the_art_of_unix_programming-1/the_art_of_unix_programming%20(1)_djvu.txt). Inspected:
  - "Pipes, Redirection, and Filters": the standard-streams convention and the filter model.
  - "Wrappers": wrapper versus shellout as specialization of a callee.
  - "Slave Processes": the state-machine cost of two-way child processes, the value of a command override for debugging, and the rule of thumb to move toward an application protocol when interaction becomes nontrivial.
  - "Process Partitioning at the Design Level": the equivalence of data-exchange mechanisms and the differences in marshalling, buffering, and atomicity.
- Not inspected: "Security Wrappers and Bernstein Chaining," "Remote Procedure Calls," and the remaining IPC method sections. This skill makes no claim based on them.

## Book-derived principles

- Programs that read standard input and write standard output can be connected without knowing their neighbors.
- Choose the least coupled mechanism that does the job.
- Two-way child processes require explicit protocol state and are hard to debug.
- Mechanism choice matters at the edges, not in the data that moves.

## Limits and dated claims

- The chapter is about processes on one Unix host and assumes shell pipelines. Network and distributed cases are not inspected here.
- The popen restriction (one direction per call) is platform behavior from that era, not a general rule.
- The client-server example is cited as an observation in the book, not as a result measured for this skill.

## Modern application

- The coupling ranking is applied to in-process calls, subprocesses, and networked services alike. The mechanisms are the same, but the failure modes (timeouts, partial failure) are handled by the reliability skill.

## Related reading not inspected

- Kernighan and Pike, *The Unix Programming Environment* (1984), the chapters on filters and the shell ([full text, archive.org](https://archive.org/stream/UNIXProgrammingEnvironment/UnixProgrammingEnvironment_djvu.txt)). Not read for this skill; the table of contents shows the relevant chapters, and they should be inspected before this skill cites them.
