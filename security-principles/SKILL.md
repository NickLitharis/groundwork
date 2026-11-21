---
name: security-principles
description: Use when changing authentication, authorization, trust boundaries, sensitive data, dependencies, or security-relevant failure behavior. Helps identify assets and principals, constrain authority, enforce policy consistently, and choose usable protections. Not a universal checklist; apply standards only within their stated scope and use existing security review workflows where required.
---

# Make security controls match the threat and boundary

Use this when a change can expose assets or grant authority. For a small change with no relevant trust boundary, do not add ceremonial threat-model paperwork. This skill complements existing secure-development and specialist review workflows; it does not replace them or require loading every principles skill.

## Model the relevant decision

Identify the assets and their harm if disclosed, altered, lost, or made unavailable. Name plausible attackers and capabilities, the principals acting for users/services/automation, the protected resources and actions, and the trust boundaries between components. Include queues, background workers, admin paths, dependency inputs, and diagnostic channels when they can affect the asset.

Write the policy in terms of who may do what to which resource and under what conditions. Identify the trusted enforcement point and evidence it needs. Do not equate same network, organization, or process origin with authorization. Verify the decision at the receiving boundary that has authority over the protected resource.

## Limit authority and exposure without creating unusable policy

Grant only the permissions and information needed for the task, for the necessary scope and duration where the system can enforce it reliably. Reduce sensitive fields passed across boundaries. Prefer a simple, reviewable policy over arbitrary fine-grained roles whose administration and consistency cannot be maintained. Least privilege reduces blast radius; it does not make an authorized vulnerable operation safe.

Choose restrictive defaults where safe, and validate against a positive domain when that domain is actually defined. An allowlist is not automatically correct for a changing or open domain. Make secure use practical; unusable controls often produce workarounds. A blocklist can be a supplemental signal, not exhaustive proof of valid input.

## Enforce all paths; add independent protection when it helps

Find every path to the protected operation: UI, API, alternate routes, batch/admin tools, async consumers, and replay paths. Ensure they use the same policy or functionally equivalent checks. Prefer a trusted shared guard when it keeps policy consistent, but test that callers cannot bypass it.

Defense in depth means controls with distinct value and preferably independent failure modes—not copying the same check into multiple places and assuming more checks equal more security. Add a second control when it addresses a separate path or failure, and account for complexity, operational burden, and user impact.

## Handle failure by protected action and domain

When authentication, authorization, integrity verification, or policy evaluation is invalid or unavailable, do not grant the protected action. That is fail-closed authorization; it does not mean shutting down every function. A bounded read-only, recovery, or emergency path is acceptable only when its authority, limits, audit, and failure behavior are designed and tested.

Define the safe state for the actual hazard. Stopping a service or denying every operation can itself cause harm. For state changes, decide whether partial work can be rolled back; do not assume a committed external effect can be undone or that retry is safe. Preserve sufficient diagnostics to investigate and recover without exposing secrets, sensitive inputs, or exploit-enabling detail to the wrong audience.

## Include dependencies and development systems proportionately

Consider a dependency a trust input: scope review to what is being introduced or changed, its source/provenance, privileges, and path to production. Protect build credentials and release authority where this change touches them. Do not turn “supply-chain security” into a demand to repeat a full audit for every unchanged package; follow the project's established inventory, scanning, and response process where applicable.

## Verify the relevant security claim

Check authorization at the enforcement boundary and across alternate paths; test both allowed and denied cases, including resource/tenant ownership and invalid or unavailable policy where applicable. Check validation at the trusted layer, restrictive defaults, secret handling in logs/errors, and the distinct value of any additional layer. For stateful business operations, test all-or-nothing behavior or the explicitly designed recovery path.

Use applicable, current requirements rather than treating a standard as universal. OWASP ASVS is scoped to web applications and web services. NIST SSDF is secure-development lifecycle guidance, not a runtime application-control catalog. As of 2026-11-21, NIST SP 800-218 v1.1 is final; the SSDF v1.2 revision is draft, so label its status if consulted. Neither prescribes arbitrary identical controls across web, embedded, native, safety-critical, or local software.

## Decision examples

- **A new endpoint returns a user's records.** Model the user/tenant as principal and records as resources; enforce ownership at the trusted server-side data boundary, not only in the UI. Check direct object-ID substitution and alternate API paths. Apply ASVS requirements only if this is within the web application/service scope.
- **An authorization service is temporarily unavailable.** Do not grant an admin operation based on a cached default. Consider a narrowly scoped read-only or emergency path only if its policy and audit are independently defined. Check that the failure does not disclose protected data or unnecessarily disable unrelated safe functions.
- **A service integration adds a dependency and diagnostic logging.** Limit credentials and fields sent; inspect dependency provenance/permissions and ensure errors do not log tokens or sensitive payloads. Check logs from failure paths, not just successful requests. Follow existing supply-chain processes instead of inventing duplicate blanket controls.

