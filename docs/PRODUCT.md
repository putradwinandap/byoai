# Product Definition

## Problem

Capable general-purpose and coding AIs can already implement software, but individual builders still perform substantial manual orchestration around them.

Common gaps include:

- context disappears across conversations;
- agents do not reliably understand current project state;
- requirements and architecture drift;
- AI-generated code is trusted too early;
- CI failures are fixed tactically but not learned from systematically;
- Git workflow, review, verification, and release require repeated human coordination;
- switching AI providers means rebuilding workflow conventions;
- specialized autonomous-development products can introduce another subscription and another ecosystem.

## Product thesis

There is value in a thin, open, model-agnostic engineering control plane that lets users bring their existing AI and surrounds it with durable context, workflow, verification, governance, and learning.

## Core value proposition

> Bring your own AI. BYOAI gives it an engineering system.

Working alternative:

> Your AI can code. BYOAI helps it engineer.

## Initial product shape

BYOAI should begin as a developer-facing CLI and repository protocol rather than a large hosted platform.

Illustrative future UX:

```bash
byoai init
byoai doctor
byoai plan
byoai run 42
byoai verify
byoai status
```

These commands are directional, not committed API contracts.

## Core capabilities to validate

### Project intelligence

Build a bounded context package from repository state, architecture, decisions, issue requirements, known failures, and engineering policies.

### Work orchestration

Convert outcomes into bounded tasks and hand them to an available AI worker without requiring BYOAI to implement its own foundation model.

### Verification

Run deterministic and independent quality gates before generated work is considered trustworthy.

### Failure learning

Record reusable lessons from failed runs and promote appropriate lessons into permanent checks or constraints.

### State continuity

Keep current project state explicit enough that a fresh AI session can continue work without reconstructing project history from chat.

### Provider adapters

Allow AI workers to be replaceable over time. Initial integrations should be selected based on what can actually be automated reliably, not on a promise to support every model immediately.

## Non-goals for early versions

- building a foundation model;
- building another IDE;
- replacing GitHub;
- replacing mature coding agents;
- replacing CI/CD platforms;
- building an enterprise management suite;
- fully autonomous production deployment before verification is trustworthy;
- optimizing for impressive multi-agent demos instead of reliability.

## Validation strategy

BYOAI should be developed from observed failures in real projects.

For a meaningful sequence of real issues, record:

1. what the human asked for;
2. what context the AI needed;
3. where human intervention was required;
4. what failed;
5. whether the failure was repeatable/preventable;
6. what permanent mechanism would prevent it;
7. how much work the AI completed autonomously.

Features should emerge from this evidence.

## Success criteria for the thesis

The thesis gains support if BYOAI can demonstrably reduce human intervention and repeated failures while keeping or improving software quality using AI tools the user already has.

The thesis should be reconsidered if mature AI platforms solve these coordination and reliability problems sufficiently without requiring a separate control layer.
