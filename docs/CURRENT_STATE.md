# Current State

**Last updated:** 2026-09-12

## Phase

Phase 0 — Discover the missing layer.

## Current thesis

BYOAI is an open, model-agnostic engineering control plane that turns an AI the user already has into part of a disciplined software-development system.

The project does **not** currently assume that another generic multi-agent coding orchestrator is needed. The working hypothesis is that the highest-value gaps are around durable context, verification, governance, failure learning, and workflow continuity.

## Current product strategy

1. Do not rush into implementation.
2. Dogfood existing AI tools on real projects.
3. Record every meaningful point where human intervention is still required.
4. Distinguish product gaps from limitations that existing tools already solve.
5. Implement the smallest reusable BYOAI mechanism that removes proven friction.
6. Measure whether it actually improves autonomy or reliability.

## Established decisions

- Name: **BYOAI** — Bring Your Own AI.
- Repository: `putradwinandap/byoai`.
- Repository is the canonical source of truth.
- BYOAI should remain model-agnostic where practical.
- Existing coding agents are workers, not competitors to be rebuilt.
- AI-generated output is untrusted until verified.
- Failure learning is a first-class differentiator candidate.
- Early target users are individual builders rather than enterprises.
- Initial implementation direction is CLI + repository protocol, subject to Phase 0 validation.

## Not decided yet

- implementation language;
- CLI framework;
- exact provider integration mechanism;
- configuration format;
- execution sandbox strategy;
- first dogfooding dataset/protocol;
- licensing;
- package/distribution method;
- hosted/cloud product strategy;
- monetization.

These are intentionally open. Future agents must not treat them as settled architecture.

## Immediate next steps

1. Define the dogfooding experiment protocol and structured run log.
2. Choose one or more real projects/issues to benchmark.
3. Establish baseline metrics before BYOAI automation exists.
4. Catalogue existing-tool capabilities to avoid unnecessary duplication.
5. From observed friction, propose the first implementation issue.

## State update rule

Whenever a meaningful issue or milestone changes the project direction, update this file in the same PR or immediately after merge.

This file should describe reality, not aspiration. Roadmap aspirations belong in `ROADMAP.md`.
