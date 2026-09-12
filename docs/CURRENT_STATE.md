# Current State

**Last updated:** 2026-09-12

## Phase

Phase 0 — Discover the missing layer.

## Current thesis

BYOAI is an open, model-agnostic engineering control plane that turns an AI the user already has into part of a disciplined software-development system.

The project does **not** currently assume that another generic multi-agent coding orchestrator is needed. The working hypothesis is that the highest-value gaps are around durable context, verification, governance, failure learning, and workflow continuity.

## Current product strategy

1. Do not rush into speculative implementation.
2. Dogfood existing AI tools on real projects.
3. Record every meaningful point where human intervention is still required.
4. Distinguish product gaps from limitations that existing tools already solve.
5. Implement the smallest reusable BYOAI mechanism that removes proven friction.
6. Measure whether it actually improves autonomy or reliability.

## Dogfooding status

The initial dogfooding protocol is established in `docs/DOGFOODING.md` with a machine-readable run template in `dogfood/RUN_TEMPLATE.yaml`.

**Dogfood Project #001 is Small.** Small will be developed under the experiment rule: human owns product intent and consequential decisions; AI performs engineering wherever tooling permits; meaningful human intervention is recorded as evidence.

The illustrative `SMALL-0000.example.yaml` is documentation only and must not be included in baseline metrics.

Evidence should be reviewed after approximately every 5 real runs, or immediately when the same preventable failure class appears twice.

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
- Small is Dogfood Project #001.
- Dogfood evidence, not feature imagination, should drive initial implementation priorities.

## Not decided yet

- implementation language;
- CLI framework;
- exact provider integration mechanism;
- configuration format;
- execution sandbox strategy;
- licensing;
- package/distribution method;
- hosted/cloud product strategy;
- monetization.

These are intentionally open. Future agents must not treat them as settled architecture.

## Immediate next steps

1. Identify/create the canonical Small repository and establish its product source of truth.
2. Select the first bounded Small engineering issue as `SMALL-0001`.
3. Capture the first real baseline run using `dogfood/RUN_TEMPLATE.yaml`.
4. Continue real runs without adding speculative BYOAI functionality.
5. Review evidence after ~5 runs or after a preventable failure class repeats twice.
6. From observed friction, propose the first implementation issue for BYOAI.

## State update rule

Whenever a meaningful issue or milestone changes the project direction, update this file in the same PR or immediately after merge.

This file should describe reality, not aspiration. Roadmap aspirations belong in `ROADMAP.md`.
