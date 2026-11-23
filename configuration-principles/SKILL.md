---
name: configuration-principles
description: Use when adding settings to a program: where they live (files, environment, flags), how they override each other, which behavior to expose, or how scripts override them. Not a configuration framework.
---

# Put each setting where its lifetime belongs

Configuration is part of a program's interface, and it is easy to add too much of it. Decide for each setting how long it should last and who should control it, then choose the mechanism that matches. Keep the precedence rules simple enough to state in one sentence.

## Match the mechanism to the setting's lifetime

Classic Unix programs read settings from a small set of places, in order of increasing locality:

1. System-wide run-control files.
2. System-wide environment variables.
3. The user's own run-control files.
4. The user's environment variables.
5. Command-line switches and arguments.

Later, more local settings override earlier, more global ones. Choose the location by how often the setting changes:

- A setting that changes on almost every run belongs on the command line.
- A setting a user keeps stable across sessions belongs in a user run-control file.
- A setting that describes the environment (paths, credentials, deployment mode) belongs in environment variables or system files.

## Make scripted behavior predictable

Provide a command-line option that overrides environment variables and run-control files. A script that passes that option behaves the same regardless of what is in a user's files. The `-e` option of `make` is a common example of this pattern.

Batch tools that act as filters or generators are usually fully configured by command-line options. Interactive programs with persistent state often rely on files and environment variables, with few options on each run. Match the pattern to how the tool is used.

## Expose fewer, better-chosen settings

Every setting is a branch in the program's behavior and a combination to test and document. Add a setting only when a real user needs to choose between behaviors that cannot be decided from context. Prefer a sensible default, and make the default's behavior visible.

## Watch for these failure modes

- A setting exposed in three places (file, environment, flag) with unclear precedence.
- Environment variables that silently override files, so a user's edits appear to have no effect.
- Settings that change behavior in ways the program does not report.
- Configuration that cannot be overridden for a single run, which makes scripted use fragile.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [interface](../interface-principles/SKILL.md) for command-line design, [minilanguage-generation](../minilanguage-generation-principles/SKILL.md) when configuration becomes a language, [portability](../portability-principles/SKILL.md) for settings that differ across platforms.
