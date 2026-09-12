# Current State

**Last updated:** 2026-09-12

## Phase

Phase 0 — Discover the missing layer and establish the safe executable foundation.

## Current thesis

BYOAI is an open, model-agnostic engineering control plane that turns an AI the user already has into part of a disciplined software-development system.

The project does **not** currently assume that another generic multi-agent coding orchestrator is needed. The working hypothesis is that the highest-value gaps are around durable context, verification, governance, failure learning, and workflow continuity.

## Current product strategy

1. Keep the repository/source-of-truth protocol as the durable foundation.
2. Begin an executable CLI with a small safe vertical slice.
3. Preserve project memory across BYOAI runtime updates and AI-provider changes.
4. Do not build speculative provider orchestration before the foundation is trustworthy.
5. Dogfood later when the product owner is ready, then use evidence to prioritize higher-level BYOAI capabilities.
6. Measure whether new mechanisms actually improve autonomy or reliability.

## Manual v0

A manually usable BYOAI workflow exists:

- `docs/QUICKSTART.md` explains end-to-end usage before a full runtime exists;
- `templates/project/` provides reusable source-of-truth scaffolding for target repositories;
- `templates/project/byoai.yaml` is a provisional machine-readable project manifest;
- `dogfood/projects.yaml` registers dogfood projects;
- `dogfood/METRICS.md` provides the initial evidence baseline.

The next product step is to automate the safest parts of this workflow through the CLI rather than replacing it with a different architecture.

## Memory and upgrade contract

The project now adopts the durable principle:

> **BYOAI owns the machinery. Your repository owns the memory.**

`docs/MEMORY_AND_UPGRADES.md` defines the ownership and compatibility contract:

- runtime-managed machinery is separate from repository-owned durable memory;
- bootstrap templates become project-owned after creation;
- runtime, protocol, and project schema versions are distinct concepts;
- installing a newer runtime does not itself migrate project memory;
- project migrations must be explicit, reviewable, validated, and recoverable;
- BYOAI must avoid memory lock-in and preserve portability across uninstall/provider changes.

The current `schema_version` in `byoai.yaml` versions the manifest representation only. A separate `protocol_version` field is deferred until evidence shows the repository needs to declare/pin it.

## CLI status

Issue #4 defines the first executable vertical slice:

- `byoai --help` / `--version`;
- safe `byoai init`;
- read-only `byoai doctor`;
- read-only `byoai status`;
- deterministic tests and local quality checks.

The first CLI must not silently upgrade or overwrite project-owned memory. Full migration machinery is not required for this slice; unsupported schemas should fail safely.

## Dogfooding status

The dogfooding protocol exists in `docs/DOGFOODING.md` with `dogfood/RUN_TEMPLATE.yaml`.

**Dogfood Project #001 remains Small, but execution is intentionally held by product-owner choice.** The memory/upgrade design prerequisite has now been defined; completing the CLI foundation is the current priority before deciding when to start Small.

The illustrative `SMALL-0000.example.yaml` remains documentation only and must not be included in baseline metrics.

## Established decisions

- Name: **BYOAI** — Bring Your Own AI.
- Repository: `putradwinandap/byoai`.
- Repository is the canonical source of truth.
- BYOAI should remain model-agnostic where practical.
- Existing coding agents are workers, not competitors to be rebuilt.
- AI-generated output is untrusted until verified.
- Failure learning is a first-class differentiator candidate.
- Early target users are individual builders rather than enterprises.
- CLI + repository protocol is the accepted first executable product direction.
- Manual v0 remains the semantic baseline the CLI should automate incrementally.
- Project repositories own durable memory; BYOAI owns runtime machinery.
- Templates bootstrap but do not synchronize over customized project files.
- Runtime, protocol, and project schema versions are distinct.
- Project migrations must be explicit and recoverable.
- BYOAI must avoid memory lock-in.
- Small remains Dogfood Project #001, but its execution is currently held.

## Not decided yet

- implementation language;
- CLI framework;
- exact provider integration mechanism;
- whether/when an explicit `protocol_version` belongs in project metadata;
- final long-term configuration/manifest schema;
- exact migration command name/UX;
- execution sandbox strategy;
- licensing;
- package/distribution method;
- hosted/cloud product strategy;
- monetization.

These are intentionally open. Future agents must not treat them as settled architecture.

## Immediate next steps

1. Complete and merge the memory ownership/versioning/safe-upgrade design contract (Issue #3).
2. Implement the first executable CLI vertical slice (Issue #4).
3. Select implementation language/framework based on CLI constraints and record the decision.
4. Add local deterministic checks before relying on CI.
5. Keep Small held until the product owner chooses to begin dogfooding.
6. When dogfooding begins, use real evidence to drive provider orchestration, failure-learning, and other higher-level features.

## State update rule

Whenever a meaningful issue or milestone changes the project direction, update this file in the same PR or immediately after merge.

This file should describe reality, not aspiration. Roadmap aspirations belong in `ROADMAP.md`.
