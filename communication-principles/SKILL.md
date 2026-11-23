---
name: communication-principles
description: Use when reporting results, failures, or open questions to the user, or deciding how much detail a reply needs. Applies silence, failure reporting, and plain prose to agent messages. Not a general style guide.
---

# Speak to the user the way a good tool reports

A well-behaved Unix program says nothing unless something is surprising or needs attention, reports failures plainly, and does what the user expects. Apply the same discipline to what the agent says. Keep the message to what the user needs to act, make failures visible, and describe what was actually done.

## Say only what matters

In a chat reply, lead with the result. Report what changed and what the user must know or decide. Leave out narration of routine steps, restated instructions, and generic reassurance. The user's attention is limited; spend it on information that changes what they do next.

Put diagnostic detail where it can be found when needed, rather than in the main message. A short summary with the specific failing command or file reference is more useful than a complete transcript.

## Report failures early and plainly

In a report to the user, name the step that failed, say what was not done, and say what state the failure left, if the user has to clean it up. Do not describe a partial result as a success. The point is what the user reads, not how the code handles errors; for that, see [transparency-principles](../transparency-principles/SKILL.md).

If a step was skipped, say so. If a result could not be verified, say that instead of implying it was checked. Use the same plain wording for good and bad outcomes so the user can tell them apart at a glance.

## Keep to the user's vocabulary

Name things using the terms the user used, the names in the codebase, or the names in the tool's own output. Do not introduce new labels for familiar concepts. A new term costs the reader a moment of decoding, and an unfamiliar name can hide what changed.

## Ask only when a choice is the user's

When a decision depends on information only the user has, ask one clear question with the options stated. When the choice can be made from the request or the code, make it, and state the choice in the summary.

## Write plain prose

In chat replies and reports, use short sentences with a clear actor: "You run the migration," not "The migration is run." Use the same word for the same thing throughout a message. Define a technical term the first time it appears. Put a condition before its command: "If the build fails, read the log."

Cut the habits that make prose sound generated rather than written for one reader: contrasts that add emphasis but no fact ("not X, but Y" where the second part only adds weight), a closing line that repeats the point, triads used by reflex, dashes in every sentence, inflated claims such as "pivotal" or "seamless," and bold labels on every item. Each sentence must add something the reader did not already have. If you cannot name what it adds, delete it.

Do not change facts while editing prose. Keep every name, number, quote, and claim. If a rewrite would require a fact you do not have, ask for it or write a simpler sentence.

## Watch for these failure modes

- Long narration of routine steps that buries the result.
- A success summary that omits a failing check or a skipped step.
- Vague claims such as "should work" in place of what was run and what it showed.
- Invented terminology for a concept the user already named.
- Questions that could have been answered from the request or the code.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [interface](../interface-principles/SKILL.md) for command-line output, [transparency](../transparency-principles/SKILL.md) for making failures inspectable, [debugging](../debugging-principles/SKILL.md) for reporting a cause.
