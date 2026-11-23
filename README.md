<h1 align="center">Groundwork</h1>

<p align="center">
  <strong>Engineering principles for coding agents.</strong><br>
  Book-grounded guidance, adapted for modern software work.
</p>

<p align="center">
  <a href="#quick-start">Quick start</a> ·
  <a href="#the-skills">The skills</a> ·
  <a href="#install">Install</a> ·
  <a href="#books-and-modern-practice">Sources</a> ·
  <a href="#evaluation">Evaluation</a>
</p>

Groundwork is a collection of twenty-four focused skills for coding agents. Each connects engineering principles to concrete decisions about scope, design, failures, data, performance, and collaboration. Use the skills with your agent's native loader or have it read the Markdown directly.

## Quick start

From a checkout your agent can read, try:

```text
Read engineering-principles/SKILL.md and follow its guidance.
Inspect this project before proposing changes. Implement the requested
behavior using its existing conventions, then verify the result.
```

Choose a skill from the catalog below, or [install the collection](#install) for native discovery. Loading and automatic selection depend on your agent.

<details>
<summary>What Groundwork asks the agent to do</summary>

- Preserve the full requirement while removing unnecessary complexity.
- Use observed evidence to distinguish explanations and evaluate changes.
- Make contracts, ownership, and failure behavior explicit.
- Follow repository conventions and protect unrelated work.

These are intended behaviors, not measured claims of improvement. Groundwork complements domain tools, security reviews, TDD, and fresh-context review workflows. Project requirements, local instructions, and observed evidence take precedence.

</details>

## The skills

Planning and engineering provide the foundations. Load specialist depth when the task needs it; a small edit does not need many skill reads or a planning document.

| Skill | Reach for it when… |
|---|---|
| [Planning](planning-principles/SKILL.md) | The outcome, scope, or sequence is unclear. |
| [Engineering](engineering-principles/SKILL.md) | You need a correct design that stays understandable. |
| [Debugging](debugging-principles/SKILL.md) | A failure needs a causal explanation. |
| [Testing](testing-principles/SKILL.md) | You need evidence that could catch a broken contract. |
| [Evolution](evolution-principles/SKILL.md) | Consumers or stored data must survive a change. |
| [Reliability](reliability-principles/SKILL.md) | Timeouts, concurrent work, overload, or recovery matter. |
| [Security](security-principles/SKILL.md) | Authority, assets, or trust boundaries are changing. |
| [Performance](performance-principles/SKILL.md) | A workload is slow, resource-heavy, or scaling poorly. |
| [Data modeling](data-modeling-principles/SKILL.md) | Identity, relationships, or the meaning of data needs care. |
| [Version control](version-control-principles/SKILL.md) | Changes need recording, integration, or safe recovery. |
| [Unix philosophy](unix-philosophy-principles/SKILL.md) | Deciding a component's scope, or whether a design has grown too large or clever. |
| [Modularity](modularity-principles/SKILL.md) | Choosing module boundaries, or judging whether a module hides its decisions. |
| [Textuality](textuality-principles/SKILL.md) | Designing a file format, protocol, or record that programs or people exchange. |
| [Transparency](transparency-principles/SKILL.md) | Making behavior inspectable, or deciding how failures should stay visible. |
| [Composition](composition-principles/SKILL.md) | Choosing how programs or components connect: pipes, subprocesses, sockets, or RPC. |
| [Minilanguage and generation](minilanguage-generation-principles/SKILL.md) | Deciding whether a problem needs a minilanguage, or whether output should be generated. |
| [Configuration](configuration-principles/SKILL.md) | Adding settings, or deciding where they live and how they override each other. |
| [Interface](interface-principles/SKILL.md) | Designing a command-line or function interface: output, errors, exit status, and scripting. |
| [Documentation](documentation-principles/SKILL.md) | Deciding what to document and how to organize it for the reader's need. |
| [Portability](portability-principles/SKILL.md) | Code must run on other platforms, runtimes, or dependency versions. |
| [Communication](communication-principles/SKILL.md) | Reporting results, failures, or questions to the user. |
| [Review](review-principles/SKILL.md) | Judging a change, repository, or design before it ships. |
| [Debt](debt-principles/SKILL.md) | Deferring work on purpose, or reviewing the deferrals already in a codebase. |
| [UI design](ui-design-principles/SKILL.md) | Designing a user interface's look, layout, motion, or the words on screen, including accessibility floors. |

The boundaries matter. Data modeling defines meaning; evolution manages a change to an existing contract. Debugging seeks causes; testing assesses behavior. Performance investigates measured costs; reliability handles operational failure. Version control manages repository history, not deployment or data rollback. Each newer skill owns one concern: unix-philosophy names the design rules, modularity owns boundaries, composition owns connections, and interface owns the user-facing contract. Engineering and planning point to these skills rather than restating them.

## Install

Groundwork is a set of Markdown instructions with bundled references. It is intended for any coding agent that can read project files or accept instructions in its context. Native skill discovery, installation paths, and invocation syntax depend on the agent; compatibility with every agent has not been tested.

### Agents with native skill support

Use your agent's documented project-local or user-wide skill directory. Copy or link each complete `*-principles/` directory there, including `references/`. Follow any additional registration requirements documented by your agent.

For a local checkout on a system with Bash and symbolic links, set `GROUNDWORK_SKILLS_DIR` to that directory, then run this snippet from the checkout root. Existing destinations are left untouched.

<details>
<summary>Link all skills from a local checkout</summary>


```bash
(
  set -eu
  source_dir="$(pwd -P)"
  skills_dir="${GROUNDWORK_SKILLS_DIR:?Set GROUNDWORK_SKILLS_DIR to the documented skill directory for your agent}"
  mkdir -p "$skills_dir"

  for skill in *-principles; do
    [ -f "$skill/SKILL.md" ] || continue
    destination="$skills_dir/$skill"
    if [ -e "$destination" ] || [ -L "$destination" ]; then
      printf 'Kept existing: %s\n' "$destination"
    else
      ln -s "$source_dir/$skill" "$destination"
      printf 'Installed: %s\n' "$skill"
    fi
  done
)
```

Reload skills or start a new session as your agent requires. Links pick up changes to this checkout; keep it at the same path. A skipped destination may be an older installation: inspect it before replacing it.

</details>

### Agents without native skill support

Ask the agent to read the relevant `SKILL.md` from this checkout and follow its guidance, loading linked practical references when needed. If the agent cannot read files, supply the relevant file contents through its supported instruction mechanism. There is no shared runtime or external package to install.

## Use

Use your agent's native skill-selection mechanism, or ask it to read a skill directly. Automatic selection is agent-dependent and not guaranteed. For example, from this checkout:

<details>
<summary>Example requests for the skills</summary>


```text
Read planning-principles/SKILL.md. Scope the CSV export and define observable acceptance.
Read engineering-principles/SKILL.md. Implement the approved design using this project's conventions.
Read debugging-principles/SKILL.md. Investigate why a timed-out payment sometimes charges twice.
Read testing-principles/SKILL.md. Review whether these tests protect the payment contract.
Read evolution-principles/SKILL.md. Plan a stored-order migration with old workers still running.
Read reliability-principles/SKILL.md. Assess this worker's timeout, retry, and recovery behavior.
Read security-principles/SKILL.md. Review tenant authorization across every path to an order.
Read performance-principles/SKILL.md. Investigate this endpoint's tail latency on a representative workload.
Read data-modeling-principles/SKILL.md. Model purchase identity, currency, and historical prices.
Read version-control-principles/SKILL.md. Integrate these branches while preserving unrelated work.
Read unix-philosophy-principles/SKILL.md. Decide whether this log-rotation feature belongs in the existing tool or a new one.
Read modularity-principles/SKILL.md. Judge whether this wrapper class hides a decision or only forwards calls.
Read textuality-principles/SKILL.md. Choose a format for the nightly export that finance can open and check by hand.
Read transparency-principles/SKILL.md. Make this batch job's failures visible to the operator without changing its output.
Read composition-principles/SKILL.md. Decide how the importer should receive records from the parser.
Read minilanguage-generation-principles/SKILL.md. Decide whether the discount rules need a language or a table.
Read configuration-principles/SKILL.md. Decide where the new retry-limit setting belongs and how it overrides defaults.
Read interface-principles/SKILL.md. Review the exit status and stderr behavior of this CLI for scripted use.
Read documentation-principles/SKILL.md. Decide which parts of this library need a tutorial, a how-to, and a reference.
Read portability-principles/SKILL.md. Isolate the file-locking code that differs between Linux and Windows.
Read communication-principles/SKILL.md. Write the final report on this migration, including what was not verified.
Read review-principles/SKILL.md. Review this change for correctness, safety, and load before it ships.
Read debt-principles/SKILL.md. Record this temporary single-process cache with its limit and the trigger for replacing it.
Read ui-design-principles/SKILL.md. Review this checkout form's contrast, error messages, and touch targets before the design is handed off.
```

</details>

Select skills for the uncertainty in the task. A migration may need evolution plus data modeling; a slow endpoint may need performance plus debugging. There is no mandatory sequence. A request for a plan or review does not authorize implementation.

## Books and modern practice

Groundwork uses original synthesis of inspected book passages and current primary documentation. Agents can use the bundled guidance without fetching the books.

For example, the newer specialists draw on:

- *The Art of Unix Programming*, Chapter 12, and *Site Reliability Engineering*, Chapters 4 and 6, for [performance reasoning](performance-principles/references/sources.md). Modern adaptations account for managed runtimes, warm-up, garbage collection, resource quotas, and workload-specific measurements.
- *Database Design*, 2nd edition, Chapters 7, 9, 11, and 12, for [data modeling](data-modeling-principles/references/sources.md). Relational dependency and integrity reasoning is qualified for APIs, documents, and events using current format and platform documentation.
- *Pro Git*, 2nd edition, selected sections on recording changes, branching, collaboration, rewriting, and recovery, for [version control](version-control-principles/references/sources.md). Modern guidance includes repository-specific tooling, protected branches, and concurrent editors or agents.

Source citations are collected here so `SKILL.md` files can focus on task guidance. Detailed source notes remain in `references/`; they identify the passages inspected, the author's advice, applicability limits, and Groundwork's adaptations. A title, contents page, or publisher summary is not a substitute for reading substantive passages. Current product documentation supports implementation details; it does not turn an old prescription into a universal rule.

Unix philosophy contributes cohesion, composition, and measurement without requiring microservices or text-only interfaces. The suite does not impose universal TDD, fixed test ratios, or function-length limits. Unreviewed DDIA second-edition chapters, inaccessible Farley design chapters, and unavailable *Tidy First?* chapters are not claimed as evidence. Check the currency and applicability of security standards before using them for compliance.

### Source index

<details>
<summary>Browse source notes for all skills</summary>


| Skill | Detailed provenance and inspected-source limits |
|---|---|
| Planning | [Planning foundations](planning-principles/references/chapter-foundations.md). |
| Engineering | [Sources and scope](engineering-principles/references/sources.md), [design foundations](engineering-principles/references/chapter-foundations.md), [complexity](engineering-principles/references/complexity.md), and [competing principles](engineering-principles/references/tradeoffs.md). |
| Debugging | [Sources and scope](debugging-principles/references/sources.md). |
| Testing | [Sources and scope](testing-principles/references/sources.md). |
| Evolution | [Sources and scope](evolution-principles/references/sources.md). |
| Reliability | [Sources and scope](reliability-principles/references/sources.md). |
| Security | [Sources, standards, and scope](security-principles/references/sources.md). |
| Performance | [Books, current documentation, and adaptations](performance-principles/references/sources.md). |
| Data modeling | [Book foundations and current format semantics](data-modeling-principles/references/sources.md). |
| Version control | [Book sections, command semantics, and collaboration policy](version-control-principles/references/sources.md). |
| Unix philosophy | [Sources and limits](unix-philosophy-principles/references/sources.md). |
| Modularity | [Sources and limits](modularity-principles/references/sources.md). |
| Textuality | [Sources and limits](textuality-principles/references/sources.md). |
| Transparency | [Sources and limits](transparency-principles/references/sources.md). |
| Composition | [Sources and limits](composition-principles/references/sources.md). |
| Minilanguage and generation | [Sources and limits](minilanguage-generation-principles/references/sources.md). |
| Configuration | [Sources and limits](configuration-principles/references/sources.md). |
| Interface | [Sources and limits](interface-principles/references/sources.md) and [CLI contracts](interface-principles/references/cli-contracts.md). |
| Documentation | [Sources and limits](documentation-principles/references/sources.md). |
| Portability | [Sources and limits](portability-principles/references/sources.md). |
| Communication | [Sources and limits](communication-principles/references/sources.md). |
| Review | [Sources and limits](review-principles/references/sources.md). |
| Debt | [Sources and limits](debt-principles/references/sources.md). |
| UI design | [Sources and limits](ui-design-principles/references/sources.md), including the WCAG and Nielsen Norman sources checked for the accessibility floors. |
| Collection plan (book sources) | [Source registry](source-registry.md), with verification method and status for each source. |

</details>

The collection plan for the book-derived skills has its own registry, which records how each source was checked: [Source registry](source-registry.md). Entries marked HTTP only were checked for response status, not content.

<details>
<summary>Planning and engineering foundations bibliography</summary>

The foundations use original synthesis informed by these sources. The linked notes above distinguish inspected passages from broader works that were not reviewed.

- [SEBoK: Project Planning](https://sebokwiki.org/wiki/Project_Planning): scope, constraints, dependencies, risk, estimation, and evolving plans.
- [SEBoK: Incremental Development](https://sebokwiki.org/wiki/Incremental_Development_Approach): feedback, learning cycles, and incremental commitments.
- [Agile Manifesto principles](https://agilemanifesto.org/principles.html): valuable working software, simplicity, feedback, and adaptation.
- Eric S. Raymond, [*The Art of Unix Programming*: Basics of the Unix Philosophy](https://cscie2x.dce.harvard.edu/hw/ch01s06.html): composition, simplicity, parsimony, transparency, prototyping, and extensibility without speculative features.
- Raymond, [*The Art of Unix Programming*](https://cdn.nakamotoinstitute.org/docs/taoup.pdf), Chapters 4, 6, 8–9, 15–16, and 18: authoritative representations, transparency, generation, project tools, reuse, and audience-specific documentation. Chapters 11–13 inform interface selection, measurement, throughput versus latency, and essential, optional, and accidental complexity. The chapter and practical-reference notes map these ideas to their inspected sections and modern applicability.
- Martin Fowler, [YAGNI](https://martinfowler.com/bliki/Yagni.html): avoiding speculative capabilities without neglecting changeability.
- Karl Wiegers and Candase Hokanson, *Software Requirements Essentials*, Chapter 1 and the Chapter 2 opening / Practice 1, in the [official publisher sample](https://ptgmedia.pearsoncmg.com/images/9780138190286/samplepages/9780138190286_Sample.pdf) and [InformIT Chapter 1](https://www.informit.com/articles/article.aspx?p=3172443&seqNum=2): need-first, iterative requirements work. Only these passages were inspected.
- David Farley, *Modern Software Engineering*, Preface and Chapter 3, “Fundamentals of an Engineering Approach,” in the [official publisher sample](https://ptgmedia.pearsoncmg.com/images/9780137314911/samplepages/9780137314911_Sample.pdf): empirical problem-solving and measurement. The design chapters were not reviewed.
- [SPACE: The SPACE of Developer Productivity](https://cacm.acm.org/practice/the-space-of-developer-productivity/) and the [DORA metrics guide](https://dora.dev/guides/dora-metrics/): measurement caveats and evolving service-level delivery measures, not individual-task scorecards.

</details>

## Evaluation

Skill structure and reference links have been validated. Automatic selection and a comparative effectiveness benefit for the suite have not been established.

Earlier local experiments evaluated engineering and planning, not the current suite. The fourteen skills added after the original ten (eleven Unix-derived skills, review, debt, and UI design) have not been evaluated at all. Several principles were also migrated into existing skills (testing, evolution, documentation, communication) after the original evaluation, so those skills no longer match the evaluated text. Research drafts, evaluation tooling, and run artifacts are excluded from the published collection.

<details>
<summary>Initial specialist smoke results (2026-11-21)</summary>

Eight specialist tasks were run with and without their applicable skill using `openai-codex/gpt-6-luna`, medium thinking. Each task had four executable checks. The table shows a fresh follow-up after correcting checker defects found in an earlier round.

| Skill | Without skill | With skill |
|---|---:|---:|
| Debugging | 4/4 | 4/4 |
| Testing | 0/4 | 4/4 |
| Evolution | 4/4 | 4/4 |
| Reliability | 0/4 | 4/4 |
| Security | 4/4 | 4/4 |
| Performance | 4/4 | 4/4 |
| Data modeling | 4/4 | 4/4 |
| Version control | 4/4 | 4/4 |
| **Total checks** | **24/32** | **32/32** |

The earlier round scored 32/32 without skills and 28/32 with skills. Its retained audit identified three failures caused by undocumented checker requirements, plus a genuine faulty generated test suite. The follow-up removed implementation-specific SKU and exception requirements and required tests to pass correct code before earning mutant-detection credit. Skills and task prompts were unchanged; original submissions and grades were retained.

This is one run per condition per task, with checker revisions informed by earlier outputs. The rounds are not interchangeable repetitions or statistical evidence of improvement. Agents deferred tests to independent checkers, so autonomous verification was not measured. Automatic selection, other models, and other agent runtimes remain untested. Full prompts, frozen inputs, outputs, audits, grading, and paired review pages are retained locally in the ignored evaluation workspace.

</details>

For a meaningful comparison:

<details>
<summary>How to compare agent runs fairly</summary>


1. Freeze the task, acceptance criteria, and project state before running either condition.
2. Use isolated copies with the same model, tools, permissions, and unrelated instructions. Record the exact skill text supplied.
3. Disable unrelated skills in both conditions using the agent's supported controls. Disabling skill discovery does not necessarily remove other instructions, stored context, or model knowledge; record what remains active.
4. Judge actual behavior, compatibility, failure handling, data preservation, and review effort. Retain failures and repeat runs before drawing stronger conclusions.

Principles mentioned, lines generated, and successful discovery are not evidence of better engineering.

</details>

## Repository map

<details>
<summary>Published files and historical names</summary>


| Path | Contents |
|---|---|
| `*-principles/SKILL.md` | Focused task guidance and skill triggers. |
| `*-principles/references/` | Deeper examples, source mappings, and evidence limits. |
| `README.md` | Installation, usage, source index, and evaluation limits. |
| `.gitignore` | Keeps local authoring research, evaluations, and generated files out of the published collection. |

Groundwork is the suite name; skill identifiers remain unchanged. Historically, `engineering-fundamentals` became `engineering-principles` and `scope-and-plan` became `planning-principles`. The eight specialists are additions, not renames of existing workflow skills. Historical evaluation artifacts retain their original names, inputs, and hashes. Use fresh workspaces for new comparisons.

</details>

## License

Groundwork's original content is available under the [MIT License](LICENSE).
Cited books and third-party material retain their respective licenses and copyrights.
