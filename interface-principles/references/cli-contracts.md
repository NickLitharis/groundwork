# CLI Contracts

Apply these conventions to tools intended for command-line automation. Adapt to the host platform and the tool's existing contract. Do not redesign an established CLI as a side effect of another change.

## Streams and composition

- Accept standard input when streaming is natural. Support explicit file operands when useful. `-` commonly denotes stdin, but follow the tool's documented contract.
- Write result data to stdout and diagnostics or progress to stderr. A successful command that produces data should not have empty stdout.
- Keep machine-readable output stable. Do not mix banners, progress, colors, or explanatory prose into JSON or other structured output. Offer a separate human-readable mode when needed.
- Do not require a terminal or prompt in unattended operation. Make interactive behavior explicit, and decide how missing credentials or confirmations fail in scripts.
- Avoid hardcoded output destinations and implicit writes. Use stdout or an explicit destination, and respect existing overwrite guarantees.
- Stream records when their semantics permit it. Bound memory for large inputs. Whole-document validation or atomic output can justify buffering, temporary storage, or a different protocol.

Do not assume that piping output makes the whole operation atomic. Define whether malformed input can leave partial stdout. For files that need all-or-nothing replacement, use a suitable atomic-write protocol and consider durability requirements. Do not promise rollback of bytes already written to a pipe.

## Failure behavior

Use zero exit status for success and nonzero for failure. Choose and document specific nonzero codes based on the CLI's contract. There is no universal mapping for application errors. Usage errors, data errors, and environmental failures may need distinct handling.

Include enough diagnostic context to act on the failure, without secrets. Handle expected downstream closure, signals, cancellation, and cleanup according to platform conventions. A broken pipe is not a reason to dump an internal traceback by default.

Validate at the appropriate boundary. On malformed input, do not quietly skip records or emit invented defaults, unless best-effort processing is an explicit mode with a documented error summary and exit policy.

## Options and configuration

Support familiar conventions where appropriate: `--help`, `--version`, and `--` to end option parsing. Use the platform's argument-parsing facilities rather than a fragile handwritten parser.

Add only the configuration sources the application needs. Precedence for those sources is owned by [configuration-principles](../../configuration-principles/SKILL.md). Keep secrets out of logs, and consider process-list exposure before accepting secrets as command-line arguments.

## Policy and mechanism

Separate parsing, domain transformation, and I/O when they have independent responsibilities or need separate verification. A few functions may be enough. Do not require separate executables or services.

Choose the simplest useful boundary: an ordinary function, a library API, a stream, a subprocess, or a network protocol. A process or service boundary adds deployment, failure, and serialization costs. Unix composability does not imply microservices. How parts connect is owned by [composition-principles](../../composition-principles/SKILL.md).

## Example

Requirement: select warning records from newline-delimited JSON, then pass the result to another tool.

```sh
select-warnings events.jsonl | summarize-warnings > report.json
```

A suitable contract: optional file operand with stdin fallback, one matching record per stdout line, diagnostics on stderr, nonzero status for invalid input, and documented partial-output semantics. Test a real pipeline as well as invalid input and a large stream. Do not add plugins or several layers of configuration to satisfy this requirement.
