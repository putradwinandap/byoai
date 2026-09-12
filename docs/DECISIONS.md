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

**Status:** accepted  
**Date:** 2026-09-12

A CLI and repository-native protocol are the first executable product surface. The CLI should automate proven repository-native workflow incrementally rather than begin as a large autonomous platform.

## D-009 — Project owns durable memory

**Status:** accepted  
**Date:** 2026-09-12

**BYOAI owns the machinery; the repository owns the memory.** Once bootstrap artifacts exist in a target repository, durable project knowledge and customizations are project-owned. Runtime updates do not authorize silent mutation or replacement of that memory.

## D-010 — Templates bootstrap; they do not synchronize

**Status:** accepted  
**Date:** 2026-09-12

Bundled templates may initialize missing project artifacts. After creation, newer templates must not silently overwrite project-owned files. Existing projects receive explicit recommendations or reviewable migrations when change is justified.

## D-011 — Runtime, protocol, and project schema versions are distinct

**Status:** accepted  
**Date:** 2026-09-12

Runtime version identifies installed BYOAI software. Protocol version describes the behavioral repository contract. Project schema version identifies machine-readable project representation such as `byoai.yaml`. A change to one does not automatically require a change to the others.

## D-012 — Project migrations are explicit and recoverable

**Status:** accepted  
**Date:** 2026-09-12

Installing/updating the BYOAI runtime must not itself migrate repository memory. A migration that mutates project-owned state requires a recoverable pre-migration state, reviewable material changes, validation, and a rollback/recovery path. Unsupported/newer schemas fail safely rather than being silently downgraded or rewritten.

## D-013 — BYOAI must avoid memory lock-in

**Status:** accepted  
**Date:** 2026-09-12

Uninstalling BYOAI or switching AI providers must leave durable project truth usable as repository-native files by humans and other AI workers. Optional future remote services must not become the sole authoritative copy of durable project memory without a new explicit architecture decision.

## Adding decisions

Add a decision when changing a durable project assumption, architecture boundary, workflow contract, or product principle. Do not log routine implementation details here.
