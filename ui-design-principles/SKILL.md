---
name: ui-design-principles
description: Use when designing or reshaping a user interface's look, layout, typography, motion, or the words on screen: buttons, labels, errors, and empty states. Guides choices that are specific to the product and its users, and warns against defaults that make an interface look templated. Not a design-system inventory, a brand guide, or a substitute for user research or accessibility audits.
---

# Make interface choices for this product, not from habit

A user interface should look like it was made for its subject. Start from what the product is, who uses it, and what they need to do. Then make deliberate choices about palette, type, layout, and motion, and keep each choice only if it serves that purpose. When the brief fixes a visual direction, follow it exactly, even if it asks for a look you would not choose yourself.

## Start from the subject

Before designing, state the product's subject, its audience, and its primary job, in a sentence or two. If the brief does not supply these, propose them and confirm. The subject's vocabulary, materials, and conventions are the best source of distinctive visual choices. A tool for accountants and a game for children should not share a visual language by default.

## Let one element carry the design

Give the interface one memorable element, usually the first thing a viewer sees, and keep the surrounding parts quiet and disciplined. Cut any decoration that does not serve the subject. Before finishing, remove one element that adds nothing.

## Use type deliberately

Choose one typeface family, or two that are clearly distinct. Set a type scale with chosen weights and spacing. Give type a visible role when it is the headline, rather than treating it as neutral text. Keep body lines short: the WCAG 2.2 recommendation (a AAA criterion, 1.4.8) is no more than 80 characters per line. Give serif body text slightly more line height than sans-serif.

Avoid the treatments that most often make a page look generated: highlighting one word in a headline, all-caps labels, and small labels placed above every heading.

## Let structure carry information

Borders, numbers, dividers, and labels should say something about the content. Use numbered markers only when the content is a real sequence, such as steps or a timeline. A card grid with the same radius, shadow, and padding on every card treats unlike content as equal; vary the treatment where the importance differs.

## Use motion for a reason

Limit motion that the user does not trigger to one deliberate moment, such as a single page-load reveal. Motion that answers the user's action, showing that something opened, expanded, or saved, is useful. Repeated entrance animations on every section and hover effects on every card add noise. Honor the user's reduced-motion setting (`prefers-reduced-motion`). WCAG 2.3.3 (AAA) makes this a criterion for motion triggered by interaction; treat it as required for any motion the user did not ask for.

## Plan, check against the brief, then build

Write a short plan first: four to six base colors with names, the typefaces and their roles, a layout concept with its alignment, and the principles that make this interface specific. Then read the plan against the brief. If a part could appear unchanged on any similar product, revise it and say what changed and why. Only then build.

## Show what the system is doing

Keep the user informed. After an action, show a result within a reasonable time: a saving indicator, a confirmation, or a progress state for anything slower than a moment. A user who cannot tell whether a click registered will click again. Predictable feedback is what lets a user trust the next step.

## Prevent errors and allow recovery

Design so that the common mistakes cannot happen: disable a submit button until the required fields are filled, or confirm only actions that cannot be undone. Where an action can be reversed, offer undo rather than a confirmation dialog. Users need a way out of any state they entered by mistake, such as cancelling a flow or leaving an edit without saving. Use good error messages as the second line of defense, not the first.

## Write the words on screen

Words in an interface exist to help someone understand and use it. Name things in the terms a user already has, not by how the system is built. Action labels should name the result: "Save changes," not "Submit." Keep one name for one action across the product, so a "Publish" button leads to a message that says "Published," and the same thing is never called two names on two screens.

Treat errors and empty states as guidance. An error says what went wrong and what to do next, without apologizing or being vague. An empty state tells the user how to begin. Keep the tone plain and matched to the audience, and let each piece of text do one job.

## Build a quality floor

Whatever the style, these are floors, not style choices. Check them on the actual screen, not an assumed layout:

- **Contrast.** Text has a contrast ratio of at least 4.5:1 against its background. Large text (18 pt, or 14 pt bold) needs at least 3:1 (WCAG 2.2 1.4.3, AA).
- **Color is not the only signal.** Errors, required fields, and status must also be shown by text, an icon, or position (WCAG 2.2 1.4.1, A).
- **Visible keyboard focus.** Every focusable element shows a focus indicator that does not disappear on a timer (WCAG 2.2 2.4.7, AA).
- **Touch targets.** Pointer targets are at least 24×24 CSS pixels, or have enough spacing around them (WCAG 2.2 2.5.8, AA). Targets of 44×44 are the AAA enhanced size and are a good default for primary touch controls.
- **Mobile width.** The layout works without horizontal scrolling at a phone's width.
- **Reduced motion.** Honored as described above.

A formal accessibility audit is a separate task; these floors are the minimum a design should meet before that audit.

## Watch for these failure modes

- Defaults that could appear unchanged on any product: a particular color scheme, card grid, or hero layout chosen without reference to the subject.
- Decoration that competes with the one element meant to stand out.
- Labels, eyebrows, or numbers that carry no information.
- Motion on every element, with none that answers an action.
- Buttons and messages whose names change partway through a flow.
- Errors that say only that something failed.
- An action with no visible result, so the user clicks again.
- Status shown only by color, such as a red border with no message.
- Touch targets smaller than 24×24 CSS pixels packed together.
- Destructive actions with no undo and no confirmation.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [communication](../communication-principles/SKILL.md) for messages from the agent to the user, [documentation](../documentation-principles/SKILL.md) for help text and reference material, [portability](../portability-principles/SKILL.md) for platform differences in layout and input.
