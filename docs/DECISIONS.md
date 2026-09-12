# Decision Log

This is a lightweight decision index for the discovery phase. As the project grows, significant decisions may move to individual ADR files.

## D-001 — Repository is the source of truth

**Status:** accepted  
**Date:** 2026-09-12

Important project context must live in version control so new AI sessions and contributors can recover state without depending on chat history.

## D-002 — Bring Your Own AI is the core product philosophy

**Status:** accepted  
**Date:** 2026-09-12

BYOAI will use existing AI models/coding agents as workers rather than attempt to build its own foundation model.

## D-003 — Prefer model-agnostic architecture

**Status:** accepted  
**Date:** 2026-09-12

Provider-specific integrations are allowed, but project-level workflow semantics should not unnecessarily depend on one AI vendor.

## D-004 — Verification precedes trust

**Status:** accepted  
**Date:** 2026-09-12

AI-generated changes are candidates until supported by sufficient verification evidence. Agent self-assessment alone is insufficient.

## D-005 — Learn from recurring failures

**Status:** accepted  
**Date:** 2026-09-12

Preventable repeated failures should result in stronger system guardrails when a reliable generalized check can be created.

## D-006 — Dogfood before building a large platform

**Status:** accepted  
**Date:** 2026-09-12

The first phase is empirical. BYOAI features should be justified by observed friction in real AI-native development rather than by speculative platform architecture.

## D-007 — Start with individual builders

**Status:** accepted  
**Date:** 2026-09-12

Initial product decisions optimize for solo developers, students, indie hackers, freelancers, and similar users who may already pay for a general-purpose AI subscription.

## D-008 — CLI + repository protocol is the current initial direction

**Status:** provisional  
**Date:** 2026-09-12

A CLI and repository-native protocol appear to be the smallest useful surface, but Phase 0 evidence may change this decision before implementation.

## Adding decisions

Add a decision when changing a durable project assumption, architecture boundary, workflow contract, or product principle. Do not log routine implementation details here.
