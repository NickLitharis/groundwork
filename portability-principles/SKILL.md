---
name: portability-principles
description: Use when code must run on other platforms, runtimes, or dependency versions; when deciding which platform features to depend on; or when isolating platform-specific code. Favors stable abstractions and open standards over perishable platform details. Not a guide to a specific cross-platform toolkit or build system.
---

# Depend on stable interfaces, not perishable details

Hardware and platforms change faster than interfaces do. Code that assumes a particular word size, byte order, operating system detail, or library version will break when any of those changes. Write to the most stable interface available, and keep the platform-specific parts small and visible.

## Write to the stable abstraction

The Unix tradition treats the operating-system interface as the stable part and the hardware as replaceable. Code that depends on details beyond the language's abstract machine model is considered poor practice, except in special cases such as operating system kernels. Ask what the stable boundary is for each dependency, and code to that boundary.

## Lean on open standards

Prefer open standards and widely implemented specifications over vendor-specific or short-lived technologies. The book's observation is that projects often outlive their expected lifetimes, so a choice that looks temporary frequently becomes permanent.

## Treat throwaway code as long-lived

Assume that a small tool will be kept longer than planned. Apply the same portability decisions to small tools as to large ones. A one-off script that hard-codes a path or a platform quirk tends to become someone's dependency.

## Isolate what cannot be portable

Some code must depend on a platform. Keep those dependencies in a small, named place, and make their assumptions explicit. Callers should not need to know which platform they run on. When a platform-specific behavior is required, document it at the point of use.

## Watch for these failure modes

- Code that assumes a word size, byte order, path separator, or locale without stating the assumption.
- Dependencies on a platform detail that the project does not control.
- Platform-specific code spread across the codebase instead of isolated.
- Choices of perishable technologies that were made for convenience and now block a change.

## Scope

The book's portability chapter is grounded in Unix history: porting between processor families, and the operating system as the stable layer. Its examples and specific claims about C, Unix variants, and standards of the 1970s through 2000s are dated. This skill does not distill them, and it does not cover modern container, cloud, or language-runtime portability, which were not inspected.

For the scope and limits of the sources, see [sources](references/sources.md). Related disciplines: [configuration](../configuration-principles/SKILL.md) for platform-dependent settings, [modularity](../modularity-principles/SKILL.md) for isolating platform code behind an interface, [evolution](../evolution-principles/SKILL.md) for changes to dependencies.
