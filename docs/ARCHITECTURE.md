# Architecture

## Status

This document defines the **conceptual architecture**, not a finalized implementation stack. Technology choices should follow experiments in Phase 0 and Phase 1.

## System model

```text
                 HUMAN INTENT
                      │
                      ▼
              ┌───────────────┐
              │ BYOAI CONTROL │
              │     PLANE     │
              └───────┬───────┘
                      │
        ┌─────────────┼─────────────┐
        │             │             │
        ▼             ▼             ▼
   Context/State   Orchestration   Policy
        │             │             │
        └─────────────┼─────────────┘
                      ▼
               Provider Adapter
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       AI/Agent A  AI/Agent B  Local/Future
          │           │           │
          └───────────┼───────────┘
                      ▼
              Untrusted Change
                      │
                      ▼
              Verification Engine
                      │
       ┌──────────────┼──────────────┐
       ▼              ▼              ▼
     Tests         Security       Review
       │              │              │
       └──────────────┼──────────────┘
                      ▼
                 Decision Gate
                  │         │
                pass      uncertain
                  │         │
                  ▼         ▼
              Git/PR     Human review
                  │
                  ▼
                Ship
                  │
                  ▼
            Failure / Outcome
                  │
                  ▼
             Learning Loop
                  │
                  └──────► Source of truth
```

## Conceptual components

### 1. Source-of-truth layer

Stores durable project knowledge such as:

- product intent;
- architecture;
- current state;
- decisions;
- engineering policies;
- known failures;
- verification requirements.

Repository-native formats are preferred initially.

### 2. Context builder

Constructs the smallest sufficient context for a task rather than blindly feeding the entire repository/history to an AI.

Responsibilities may include:

- identifying relevant source-of-truth documents;
- selecting relevant code and history;
- injecting issue acceptance criteria;
- including known failure patterns;
- applying token/context budgets.

### 3. Orchestrator

Controls bounded task execution.

Responsibilities may include:

- task lifecycle;
- provider selection;
- permission boundaries;
- retry limits;
- escalation;
- verification sequencing;
- state transitions.

### 4. Provider adapters

Normalize interaction with external AI workers.

BYOAI should avoid assuming every provider exposes identical capabilities. Adapters should expose capability metadata rather than pretending all providers are interchangeable in every dimension.

### 5. Verification engine

Treats AI output as a candidate change.

Possible evidence sources:

- formatting/linting;
- compilation/build;
- unit tests;
- integration tests;
- end-to-end tests;
- static security analysis;
- dependency checks;
- architecture rules;
- independent AI review where deterministic checks cannot fully cover semantics.

Independent AI review is supporting evidence, not a replacement for deterministic verification.

### 6. Policy engine

Determines what actions are permitted based on evidence and risk.

Examples:

- low-risk documentation change may be auto-committable;
- authentication changes may require stronger tests;
- destructive database changes may require human approval;
- production deployment may remain manual until sufficient evidence exists.

### 7. Failure-learning layer

Captures failures in structured form and determines whether they should produce:

- a regression test;
- a lint/static rule;
- a workflow validation;
- a provider instruction;
- a source-of-truth update;
- an architecture decision;
- no permanent action if the failure is non-generalizable.

The learning mechanism should be auditable. BYOAI must not silently mutate important policy based only on an AI judgment.

### 8. Git/CI integration

Git remains the primary change ledger. GitHub is the first intended collaboration target, while core concepts should avoid unnecessary GitHub-only coupling.

## Security model

Assume AI workers can make mistakes and can be influenced by repository content.

Early architecture should therefore favor:

- least privilege;
- bounded filesystem/repository scope;
- explicit secret isolation;
- sandboxed execution where practical;
- command allow/deny policy;
- auditable actions;
- no autonomous destructive action without policy authorization.

## Architecture rule

Do not add a subsystem merely because an autonomous platform could theoretically need it. Every major component must be justified by an observed use case or a near-term experiment.
