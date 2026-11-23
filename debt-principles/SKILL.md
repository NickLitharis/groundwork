---
name: debt-principles
description: Use when deliberately deferring work with a shortcut, recording a known limitation in code, or reviewing deferrals already in a codebase. Covers each shortcut's limit and upgrade trigger. Not when to take a shortcut.
---

# Record every deferral with its limit and its trigger

A shortcut is a decision to build less now. It is safe only while its limit holds, and it stays a decision only while someone can find it. Record each deliberate shortcut where its code lives, name the limit it works under, and name the condition that means it must be revisited. A deferral without a recorded limit and trigger is a hidden defect waiting for its load.

## Record the shortcut where it lives

Put the marker in a comment next to the simplified code. Name three things: what was simplified, the ceiling (the limit under which it is correct), and the upgrade path (the trigger that means it must change). A marker such as `shortcut: <what>, ceiling: <limit>, upgrade: <trigger>` is enough. Use the project's comment syntax, and the same marker word everywhere in the project so it can be searched.

A ceiling is a concrete bound: a row count, a request rate, a single process, a supported platform. A trigger is an observable event: the table passes a stated size, a second writer is added, a customer requires the feature. "Later" and "when we have time" are not triggers.

## Keep a ledger you can read

Gather every marker into one list, grouped by file, with its ceiling and trigger. Use the ledger to see what is deferred and whether any marker has no trigger. Review it when the project changes shape: a new deployment target, a new consumer, a large increase in data or traffic. A ledger that nobody reads does not prevent debt, so put it where the people who change the code will see it.

## Treat a crossed ceiling as a defect

When the expected load passes a shortcut's ceiling, the shortcut is no longer a decision. It is a defect to fix before the load arrives, not after. Check the ledger against the load you expect, not only against the load you have now. A shortcut whose trigger has already happened should be reported as due, not left in place.

## Do not record what is not a deferral

A marker is for a deliberate, bounded simplification. Ordinary notes, reminders of a keyboard shortcut, and TODOs with no limit are not debt entries. Keep the marker word specific enough that prose which merely mentions it is not counted.

## Watch for these failure modes

- A shortcut with no ceiling or no trigger, which rots silently.
- A ledger that is generated once and never checked against the current load.
- A crossed ceiling that stays in the code because nobody re-read the ledger.
- Markers used as a general TODO list, so real deferrals are lost among trivial notes.
- Treating a recorded shortcut as permission to ignore the limit.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [engineering](../engineering-principles/SKILL.md) for whether a shortcut is justified, [planning](../planning-principles/SKILL.md) for scheduling deferred work, [performance](../performance-principles/SKILL.md) for measuring whether a ceiling has been reached, [documentation](../documentation-principles/SKILL.md) for keeping the ledger readable.
