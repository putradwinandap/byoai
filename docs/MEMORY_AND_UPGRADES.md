# Memory Ownership and Safe Upgrades

## Status

Accepted design contract for the Phase 0/CLI foundation. Implementation may refine mechanics, but must preserve these safety properties unless a later explicit decision supersedes them.

## Core principle

> **BYOAI owns the machinery. Your repository owns the memory.**

BYOAI may provide tools, schemas, defaults, validators, migrations, and bootstrap templates. Durable project knowledge belongs to the project and must not depend on a particular BYOAI installation, AI provider, hosted account, or chat history to remain usable.

## What counts as project memory

Project memory includes durable knowledge required for a human or fresh AI worker to understand and continue the project, including:

- vision and product intent;
- architecture and constraints;
- accepted decisions;
- current state and next steps;
- project-specific workflow/rules;
- lessons and failure history;
- experiment/run history when stored in the target project;
- user customizations to generated bootstrap documents;
- other repository-native knowledge explicitly declared by the project.

Project source code and normal application data are also project-owned, but this contract focuses on engineering memory/protocol artifacts.

## Ownership classes

### 1. Runtime-managed machinery

Owned by the installed BYOAI distribution, not copied as mutable project memory:

- CLI executable and libraries;
- built-in validators;
- migration implementations;
- default schemas;
- bundled bootstrap templates;
- provider adapters;
- verification/orchestration implementation.

Updating the runtime may replace these installed assets. It must not imply permission to rewrite project-owned files.

### 2. Project-owned memory

Once material exists inside a target repository, it is project-owned unless explicitly documented as generated disposable output.

Examples:

- `AGENTS.md`;
- `docs/VISION.md`;
- `docs/PRODUCT.md`;
- `docs/ARCHITECTURE.md`;
- `docs/CURRENT_STATE.md`;
- `docs/DECISIONS.md`;
- `docs/WORKFLOW.md`;
- project lessons/failure/run logs;
- project-specific configuration values.

BYOAI may read, validate, propose edits, or migrate these artifacts according to this contract. It must not silently replace them from newer templates.

### 3. Project protocol metadata

`byoai.yaml` is project-owned configuration interpreted by BYOAI. Its format is versioned. BYOAI may validate it and may propose migrations, but the committed file belongs to the repository.

### 4. Generated disposable state

Future caches, indexes, temporary plans, lock-like runtime metadata, downloaded artifacts, and other reproducible state may be BYOAI-managed when clearly identified as disposable. Such state must not be the only copy of durable project knowledge.

A future implementation must document generated/disposable paths before relying on this class.

## Bootstrap template rule

Templates are **bootstrap material, not synchronization targets**.

`byoai init` may create project-owned files when they do not already exist. After creation, those files belong to the project. A newer BYOAI template does not become authoritative over them.

Therefore:

- `init` must not silently overwrite an existing project-owned file;
- runtime upgrades must not re-copy templates over project files;
- improvements to templates affect newly initialized projects by default;
- existing projects may receive explicit upgrade recommendations or migration proposals;
- customized project files are expected and must be preserved.

## Three independent versions

BYOAI distinguishes three concepts.

### Runtime version

The installed BYOAI software release, for example `0.3.1`.

Runtime releases can change implementation without changing the project protocol. A runtime update alone does not authorize repository mutation.

### Protocol version

The behavioral contract between BYOAI and a repository: ownership rules, required concepts, command semantics, compatibility expectations, and interpretation of project metadata.

Protocol changes are intentional product/architecture changes. A runtime may support more than one protocol version during a compatibility window.

### Project schema version

The machine-readable representation used by a project, initially represented by `schema_version` in `byoai.yaml`.

Schema version changes only when machine-readable project data requires a migration. Documentation/template wording changes do not automatically require a schema bump.

## `byoai.yaml` v1 interpretation

The current draft remains intentionally small:

```yaml
schema_version: 1

project:
  name: "example"
  repository: "owner/example"

source_of_truth:
  agents: "AGENTS.md"
  vision: "docs/VISION.md"
  product: "docs/PRODUCT.md"
  architecture: "docs/ARCHITECTURE.md"
  current_state: "docs/CURRENT_STATE.md"
  decisions: "docs/DECISIONS.md"
  workflow: "docs/WORKFLOW.md"

verification:
  required: []

policy:
  human_approval_required_for: []
```

`schema_version` versions the manifest representation, not the BYOAI runtime. The runtime version must not be written into the manifest merely to track which CLI last touched the repository.

A future explicit `protocol_version` field may be introduced if dogfooding demonstrates that repositories need to pin/declare protocol semantics independently from schema representation. Until then, protocol compatibility is a runtime/documented contract and must not be inferred from `schema_version` alone.

## Compatibility rules

| Situation | Default behavior |
| --- | --- |
| Runtime patch/minor update; supported schema/protocol unchanged | Read/use project without mutation. |
| New runtime understands project's older schema/protocol | Operate in compatible mode; optional upgrade may be offered. |
| Runtime introduces new optional template/rule | Do not overwrite project files; surface recommendation if useful. |
| Project schema migration is required | Refuse mutating commands that require the new schema until explicit migration succeeds. Read-only diagnosis should remain available where practical. |
| Project schema is newer than runtime understands | Fail safely with actionable compatibility message; never downgrade automatically. |
| Protocol semantics are incompatible | Require explicit upgrade/migration path or compatible runtime; no silent reinterpretation. |
| Unknown fields are safe to preserve | Preserve them through migration where practical; never discard unknown project data merely for convenience. |

Backward compatibility should be preferred when its complexity is reasonable. Compatibility windows and deprecation policy can be defined once real released versions exist.

## Safe migration protocol

A migration that changes committed project-owned state must follow this conceptual sequence:

```text
inspect
  ↓
preflight compatibility + clean/safe working-state checks
  ↓
backup / recoverable snapshot
  ↓
generate proposed migration
  ↓
show material changes / diff
  ↓
explicit authorization when project-owned state will change
  ↓
apply migration
  ↓
validate new schema + source-of-truth invariants
  ↓
run relevant deterministic verification
  ↓
success → retain auditable change
failure → rollback/recovery path
```

### Safety requirements

- Never perform a destructive migration silently.
- Never treat template content as more authoritative than customized project memory.
- Do not delete unknown user content merely because the new schema does not recognize it.
- Create a recoverable pre-migration state before mutating project-owned memory.
- Validate after migration before declaring success.
- If validation fails, leave the user with either the original state restored or an explicit recoverable state and instructions; never claim success.
- Prefer migrations represented as normal repository diffs/commits/PRs so users and AI reviewers can inspect them.
- Do not require network access merely to preserve local project memory.

## Upgrade UX

The intended future command separation is:

- package manager/runtime mechanism updates the BYOAI executable;
- `byoai doctor` diagnoses runtime/project compatibility;
- `byoai status` reports detected project/schema/protocol status;
- a future explicit command such as `byoai migrate` or `byoai upgrade-project` proposes project changes.

Installing a newer CLI must **not** itself mutate repository memory.

For Git-backed projects, project upgrades should prefer a reviewable diff and may optionally create a branch/commit/PR. Exact CLI names and automation level remain implementation decisions.

## Rollback and recovery

Before a migration mutates project-owned state, BYOAI must establish a recovery mechanism appropriate to the environment. Git history may be part of recovery but must not be blindly assumed sufficient, for example when the working tree contains uncommitted user changes.

The migration implementation should:

1. detect unsafe/conflicting working state;
2. avoid overwriting uncommitted project work;
3. preserve a pre-migration snapshot or equivalent recoverable representation;
4. validate the migrated result;
5. restore or provide deterministic recovery if application/validation fails.

The first CLI vertical slice does not need to implement full migrations. Until migration support exists, it should fail safely when an unsupported schema would require mutation.

## Portability and uninstall contract

BYOAI must avoid memory lock-in.

After uninstalling BYOAI:

- source-of-truth documents remain ordinary repository files;
- a human can read them;
- another AI worker can read them;
- Git history remains meaningful;
- project knowledge does not disappear because a BYOAI service/account is unavailable.

Switching from one AI provider to another must not require rewriting project memory solely because the provider changed. Provider-specific hints may exist in the future, but durable project truth must remain provider-neutral wherever practical.

BYOAI may eventually offer optional remote capabilities, but remote state must not become the sole authoritative copy of durable project memory without a new explicit architecture decision.

## Scenario verification

### Scenario 1 — runtime patch update, no protocol change

`0.3.0 → 0.3.1`. The runtime replaces its own executable/library assets. Project files remain byte-for-byte untouched unless the user separately runs an explicit project mutation command.

**Expected:** safe; no migration.

### Scenario 2 — protocol evolves but current project remains compatible

New runtime adds an optional verification recommendation while still understanding the existing project contract.

**Expected:** project continues to work. BYOAI may recommend the improvement but cannot overwrite `AGENTS.md` or other project memory.

### Scenario 3 — schema migration required

A future manifest representation cannot be safely interpreted as v1.

**Expected:** diagnosis/read-only behavior where possible; mutating behavior requiring the new representation is blocked until an explicit migration is reviewed and succeeds.

### Scenario 4 — migration validation fails

Migration writes an invalid manifest or violates source-of-truth invariants.

**Expected:** do not report success. Restore the recoverable original state or provide deterministic recovery from the preserved snapshot.

### Scenario 5 — customized generated files

User heavily edits the `AGENTS.md` originally produced by `byoai init`.

**Expected:** it is project-owned. New template versions never silently replace it. An upgrade may propose a diff.

### Scenario 6 — uninstall BYOAI / switch provider

User removes the CLI and moves from Codex to another AI worker.

**Expected:** project memory remains in repository-native files and continues to be understandable. Provider change does not invalidate project truth.

## Consequence for the first CLI

Issue #4 may safely implement `--version`, `init`, `doctor`, and `status` under this contract.

For the first vertical slice:

- `init` creates only missing bootstrap files and fails safely on conflicting existing files;
- `doctor` is read-only;
- `status` is read-only;
- unsupported/newer schemas produce actionable errors;
- no command silently upgrades project memory;
- full migration implementation is deferred until evidence requires it.

This lets BYOAI become executable without putting project memory at risk.