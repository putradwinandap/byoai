# Roadmap

The roadmap is evidence-driven. Later phases are directional and may change as dogfooding exposes what existing AI tools already solve well.

## Phase 0 — Discover the missing layer

**Goal:** prove that BYOAI solves real gaps rather than rebuilding existing AI products.

- Establish repository source of truth.
- Define the BYOAI thesis, principles, and conceptual architecture.
- Select real dogfooding projects.
- Define an experiment log for AI-assisted issue execution.
- Track human interventions, failures, repeated failures, and verification gaps.
- Study which capabilities existing AI/coding-agent products already provide sufficiently.
- Identify the smallest high-value control-plane feature.

**Exit criteria:** at least one repeated, meaningful workflow/reliability problem is demonstrated across real development work and is not adequately solved by the underlying AI worker alone.

## Phase 1 — Repository protocol + CLI skeleton

**Goal:** make a repository BYOAI-aware without building a full autonomous runtime.

Candidate scope:

- `byoai init`;
- machine-readable project manifest;
- source-of-truth conventions;
- `byoai doctor` validation;
- current-state representation;
- structured failure/lesson format;
- policy/config schema;
- local deterministic checks.

**Exit criteria:** a fresh AI session can inspect a BYOAI repository and reliably recover the project's operating context with minimal human explanation.

## Phase 2 — Verification-first task runner

**Goal:** execute bounded tasks and verify outcomes.

Candidate scope:

- task representation;
- context builder;
- bounded execution lifecycle;
- verification pipeline;
- retry budget;
- failure classification;
- human escalation;
- execution audit log.

**Exit criteria:** BYOAI can run a bounded engineering task through at least one AI worker and produce evidence explaining why the result should or should not be trusted.

## Phase 3 — Bring Your Own AI adapters

**Goal:** demonstrate genuine provider independence.

- capability-based provider interface;
- first supported provider/agent integration;
- second materially different provider integration;
- provider-specific capability detection;
- fallback/escalation rules where useful;
- cost and execution telemetry where available.

**Exit criteria:** the same BYOAI task protocol can be executed through at least two AI workers without changing project-level workflow semantics.

## Phase 4 — Failure learning

**Goal:** make repeated avoidable failures trend downward.

- structured failure memory;
- regression-rule proposals;
- safe promotion of lessons into permanent checks;
- repeated-failure detection;
- verification-gap analysis;
- metrics dashboard/reporting.

**Exit criteria:** measured dogfooding demonstrates that previously observed preventable failure classes are caught earlier or eliminated.

## Phase 5 — GitHub-native autonomous loop

**Goal:** reduce human coordination across issue → change → PR.

- GitHub issue ingestion;
- branch/commit/PR lifecycle;
- CI evidence ingestion;
- risk-aware merge readiness;
- source-of-truth updates;
- human approval boundaries.

Auto-merge is optional and must be earned by verification maturity.

## Phase 6 — Ship and observe

**Goal:** connect verified engineering work with delivery outcomes.

Potential scope:

- deployment adapters;
- preview validation;
- release policy;
- rollback evidence;
- production signals feeding future tasks;
- escaped-defect tracking.

## Phase 7 — Software factory

**Goal:** support increasingly autonomous multi-task product development without sacrificing auditability or reliability.

Possible capabilities:

- parallel bounded work;
- dependency-aware scheduling;
- risk-aware agent assignment;
- automatic issue decomposition with review gates;
- continuous verification;
- autonomy metrics;
- self-improving project guardrails.

This phase is deliberately last. BYOAI should earn the term "software factory" through reliability, not through a multi-agent demo.

## North-star metrics

- Human intervention rate ↓
- Repeated preventable failure rate ↓
- Escaped defect rate ↓
- Mean task cycle time ↓
- Cost per verified task ↓
- Successful autonomous task rate ↑
- Verification coverage/evidence quality ↑
