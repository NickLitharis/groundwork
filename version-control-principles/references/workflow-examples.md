# Workflow examples and decision checks

These examples illustrate decisions, not a universal command sequence. Prefer repository-specific tooling and policy. Git commands are examples only; do not run them when the task or local workflow calls for another interface.

## Select a safe commit scope

Suppose a task edits `src/parser`, while a collaborator has staged work and another process edits documentation. First inspect repository guidance, status, and staged/unstaged diffs. If the shared index or working tree is active, coordinate before changing it; the index is shared by users of the same worktree, not private to an agent or editor. If the task owns a separate worktree/index, select only intended paths or hunks, then inspect the exact staged patch before recording it. Refresh the status and staged diff immediately before commit because state may have changed since inspection. Do not stash, reset, clean, or broadly stage just to simplify the workspace.

For Git, `git add -p src/parser.c` can select hunks, while a broad pathspec may also stage deletions or other eligible content. Neither is intrinsically safe: inspect its result. A later edit to a staged file changes the working tree, not the already-staged snapshot. Re-stage only the intended new content, and leave other edits unstaged.

## Make a reviewable snapshot

Suppose a feature and an unrelated formatting migration happen together. Separate them if each change can stand alone and independent review or rollback matters; keep them together if splitting would leave a misleading or invalid intermediate state. Prefer a message that names the behavior and explains a non-obvious reason, while following the repository’s subject format, trailers, signing, and commit tooling. A fixed commit size or universal imperative style is not a substitute for local convention.

## Choose integration style by policy

A team with continuous integration may prefer short-lived contributions; a product with supported release lines may keep longer-lived branches; another group may commit directly to a protected shared mainline. Follow how this repository actually reviews, checks, releases, and supports changes. If a required pull request, approval, status check, merge queue, or signing rule exists, do not bypass it with a local merge or direct push.

Merge retains the explicit joined ancestry. Rebase replays commits and gives them new identities. Rebase private work only if it fits local policy and nobody depends on its old commit IDs. If a push is rejected because the remote advanced, fetch and integrate according to the project workflow; do not force-push to make the rejection disappear.

## Resolve by behavior, then verify

Two changes alter a timeout: one converts seconds to milliseconds; another changes the default. A textual resolution can compile while making the timeout 1,000 times longer or shorter. Read both patches, callers, units, and expected behavior; resolve the intended value and contract, then inspect the full result. Run relevant behavior tests and repository-required checks on the integrated state, and inspect generated files or migrations if applicable. Do not mark a conflict resolved merely because markers are gone or compilation succeeds.

## Investigate history without overclaiming

A blamed line points to a refactor, but that change may only have moved the line. Inspect its patch and surrounding history, follow renames where useful, and check callers/current behavior. For bisect, define a reproducible property and known-good/bad revisions. The result is a boundary under those assumptions, not independent proof of causation.

## Recover based on what is at risk

If a published change should be undone, a revert commit often preserves the shared record; confirm repository policy, especially for merge commits. If an unshared local commit needs editing, amend or rebase only after confirming it is not depended on and the project permits it. Reset, restore, and clean operations can change or delete data; their effects depend on mode and path selection. Inspect and preserve staged, unstaged, untracked, ignored, and concurrent files first. If intent, ownership, or recoverability is unclear, stop and coordinate rather than discard anything.

A reflog may identify a recent local reference position after a commit or branch pointer moved. It is local and expires; it is not a backup and does not restore uncommitted or untracked file contents. Preserve important files separately before risky recovery and follow the project’s recovery process.

## Handle sensitive and generated files

Before staging credentials, local configuration, build output, generated sources, fixtures, or data dumps, check repository policy and identify the authoritative source. Do not commit secrets; if one entered history, treat it as exposed and follow the incident process. Include generated output only when the repository expects it. Ignore rules do not remove files already tracked.
