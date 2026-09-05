---
name: right-size-change
description: "Calibrate the investigation, implementation, and verification scope of a software change so it is complete without becoming speculative or unnecessarily broad. Use when scope is uncertain, local and structural solutions compete, completeness and minimality are in tension, cross-boundary impacts are plausible, or evidence suggests the original change boundary may need expansion. Apply while planning or implementing features, bug fixes, refactors, migrations, or maintenance under those conditions. Avoid for fully specified mechanical edits with obvious impact, read-only simplification review, open-ended architecture design with no concrete change, or non-software work."
---

# Right-Size Change

Deliver the smallest complete change supported by current requirements and evidence.

Keep the inspection scope wider than the mutation scope. Inspect enough context to find real
impacts, but do not treat inspected code as permission to change it.

## Calibrate The Change

### 1. Establish The Contract

Identify:

- the requested outcome and completion conditions
- explicit scope, protected behavior, compatibility promises, and repository constraints
- material unknowns that could change the result, risk, or public contract

Infer routine details from repository evidence when assumptions are local and reversible. Ask or
stop when an unresolved choice would materially broaden the change, alter a public contract, or
require new authority.

### 2. Locate The Primary Change Level

Use these levels to locate the requested change:

- **Macro:** product intent, system responsibilities, major architecture, operations, or
  cross-system constraints
- **Meso:** module boundaries, APIs, data models, workflows, ownership, or dependency direction
- **Micro:** functions, types, branches, queries, configuration, tests, or local behavior

Treat the level as navigation, not permission to change other levels.

### 3. Set The Initial Mutation Boundary

From current evidence, provisionally distinguish:

- **required surfaces:** files, contracts, tests, or documentation that must change
- **protected surfaces:** behavior, APIs, schemas, boundaries, dependencies, or unrelated code that
  should remain stable
- **adjacent checks:** callers, callees, state transitions, failure paths, integrations, or
  operational effects that may need inspection but not modification

Do not report level, radius, boundary labels, or routine calibration. Surface only a material scope
decision or approval need.

### 4. Select The Inspection Radius

Choose the smallest radius that can reveal plausible impacts:

- **Direct:** inspect the target and focused verification when impact is self-contained
- **Adjacent:** inspect relevant callers, callees, contracts, state, failures, and integrations when
  the change may cross a local boundary
- **Broad:** inspect representative workflows, components, compatibility, migration, and operations
  when evidence crosses system boundaries

Treat level and radius as independent axes: level describes where the change occurs; radius
describes how far evidence requires inspection.

After inspection, and whenever implementation reveals material evidence, keep, narrow, or expand
the mutation boundary. Apply the expansion criteria before broadening it. Do not perform a full
repository, architecture, security, or performance review by default.

## Choose The Smallest Complete Solution

Treat the requested scope, repository constraints, current contracts, and safety-relevant
invariants as hard constraints. Among solutions that satisfy them:

- fulfill the current contract, including relevant failures, boundaries, cleanup, and compatibility
- follow suitable existing patterns and capabilities
- add no option, abstraction, dependency, layer, or public surface without current evidence
- keep unrelated cleanup and hypothetical future work separate

Minimize unjustified maintenance surface, not changed lines. A larger direct fix is preferable to a
smaller patch that duplicates policy, hides a known failure, or leaves inconsistent state.

## Control Scope Expansion

Broaden the mutation boundary only when:

- the user requested the broader change
- correctness, safety, or an existing contract cannot be preserved inside the current boundary
- repository evidence shows a structural cause that must be addressed to complete the current
  outcome

Use the narrowest evidence-backed expansion. Make a material change to outcome, public contract,
migration burden, risk, or user-visible behavior visible before acting unless already authorized.
Do not expand for nearby cleanup, conceivable reuse, or hypothetical requirements.

## Verify Both Directions

Use these as risk-selected lenses, not an exhaustive checklist. Apply only what the affected
contract and plausible impact support.

Check for under-engineering:

- satisfy the completion conditions and relevant success, failure, boundary, and state behavior
- keep affected callers, integrations, contracts, tests, types, schemas, configuration, and
  documentation consistent where applicable
- keep material assumptions and verification gaps visible

Check for over-engineering:

- require a current task-backed reason for every changed surface and new concept
- exclude speculative flexibility, duplicate mechanisms, and unrelated refactoring
- remove expired scaffolding and keep verification proportionate to actual impact

Finish when the contract is met, material impacts indicated by the selected radius are checked,
relevant verification passes, and further work would address only hypothetical or unrelated
concerns.

## Keep The Responsibility Bounded

Own scope calibration, expansion decisions, and proportionate completion checks. Do not prescribe
specialized implementation, testing, architecture, security, performance, or review methods; apply
the relevant project or domain guidance separately when one becomes the primary task.