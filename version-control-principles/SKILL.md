---
name: version-control-principles
description: Apply safe, reviewable version-control practices when editing a repository, staging or committing work, choosing branches or integration methods, resolving conflicts, inspecting history, or recovering from mistakes. Preserve unrelated work and shared history; follow repository-specific contribution and commit procedures before generic Git habits.
---

# Version Control Principles

Use version control to make changes understandable, reviewable, and recoverable. These principles apply to Git examples; adapt them to the repository’s actual VCS.

## Follow the repository’s workflow

Before changing repository state, read its contribution instructions, automation, branch protections, and task-specific requirements. Use the prescribed VCS interface and commit/PR tool first; do not substitute generic Git commands, commit directly, bypass required checks, or impose a message/branch convention when local policy says otherwise.

## Know what will be recorded

In Git, `HEAD` is the current committed snapshot, the **index** is the exact proposed next snapshot, and the **working tree** contains files currently checked out and edited. Untracked files are not in either snapshot. Inspect status plus staged and unstaged diffs before changing or recording state. A later edit to a staged file does not update the index automatically; stage it again only if that edit belongs in the proposed commit.

Stage only the task’s paths or hunks. Review the staged diff—including deletions, renames, generated output, and sensitive data—before recording it. Prefer explicit path/hunk selection over broad staging when other work may be present. A shared working tree or index can change between inspection and commit: refresh status/diffs before acting, avoid racing another editor or agent, and coordinate rather than assuming your earlier view is still current. Never reset another person’s index or overwrite edits to create a clean slate.

Make each commit a coherent, useful snapshot. Keep changes together when they implement one inseparable behavior; separate independent changes when that improves review or rollback. Explain the change and any non-obvious reason in the message, following project convention rather than a universal size or wording rule.

Ignore rules do not untrack files already committed. Check repository policy before including credentials, local configuration, private data, generated output, or build artifacts. If a secret entered history, treat it as exposed and follow the incident process; deleting it later does not revoke it.

## Integrate according to collaboration policy

Choose branch length and integration style to fit the team’s review, release, deployment, and support needs. Topic branches, long-lived branches, direct shared-mainline work, and other models can each fit; do not mandate Gitflow, trunk-based development, or any named branch structure.

A merge preserves the joined ancestry; a rebase replays commits and changes their identities. Decide using repository policy and whether anyone may depend on those commits. Rewrite only history you control, or after explicit coordination with everyone affected. Never rewrite shared/published history, force-push, or change a shared branch without explicit authorization and coordination. A rejected push is a signal to fetch and integrate others’ work under local policy, not to force past it.

Resolve conflicts by understanding both sides’ intent and the domain behavior—not by choosing “ours” or “theirs” mechanically. Textual conflict resolution can compile yet violate a unit, invariant, API contract, ordering rule, or migration expectation. Inspect the complete integrated diff and relevant callers, data, tests, and generated artifacts; run the repository’s required checks against the integrated result before declaring it sound. A conflict-free merge or green check alone does not establish semantic correctness.

## Use history as evidence

Use log, diff, blame, and bisect to investigate changes. Inspect context, renames, merges, and the property tested: blame attributes a line to a revision, not necessarily its cause; bisect locates a transition only under the supplied good/bad assumptions. Verify conclusions against current code and behavior.

## Recover without discarding work

Choose recovery based on what must be preserved and who depends on the history. Revert generally records a new change that counteracts an existing commit; reset moves a branch and, depending on mode, also changes the index or working tree. Restore can replace selected index or working-tree contents. All can have different effects than their names suggest. Before any state-changing recovery, inspect staged, unstaged, untracked, ignored, and shared work; preserve anything important and stop to coordinate when ownership or intent is unclear.

Do not run destructive cleanup, overwrite user changes, discard uncommitted work, force-push, or rewrite shared history without explicit authorization and coordination. A commit records tracked staged content—not untracked or unstaged files—and is not a backup. A reflog may help find recent local reference movements, but it is local, expires, and cannot recover arbitrary never-committed edits. Do not promise recovery; preserve data first and use the project’s recovery process.

For conditional examples, see [references/workflow-examples.md](references/workflow-examples.md).