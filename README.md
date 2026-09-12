# BYOAI

**Bring Your Own AI. Turn it into a software engineering system.**

BYOAI is an open, model-agnostic control plane for AI-native software development.

Instead of replacing ChatGPT, Codex, Claude, Gemini, local models, or future coding agents, BYOAI gives the AI you already use the structure required to behave like a disciplined software engineering team.

## Why BYOAI exists

Modern AI can already write a lot of code. The harder problem is everything around the code:

- preserving project context across sessions and agents;
- turning product intent into an executable engineering plan;
- keeping architecture and decisions consistent;
- validating AI-generated changes before they are trusted;
- preventing the same CI and implementation failures from recurring;
- making GitHub, tests, review, release, and deployment part of one repeatable loop.

BYOAI focuses on that system.

## Core idea

```text
Human intent
    ↓
BYOAI control plane
    ↓
AI provider / coding agent
    ↓
Untrusted implementation
    ↓
Verification + quality gates
    ↓
GitHub / CI / review
    ↓
Ship
    ↓
Learn from failures
    ↺
```

The intelligence can come from whatever AI the user already has. BYOAI provides the engineering operating system around it.

## Use BYOAI today — Manual v0

BYOAI is currently a protocol and source-of-truth system, not yet an installable CLI/runtime.

The usable loop today is:

1. bootstrap a target repository from `templates/project/`;
2. replace template placeholders with real product/architecture/current-state information;
3. define bounded work as a GitHub issue;
4. give your existing AI the repository operating contract in `AGENTS.md`;
5. let AI implement the issue;
6. run the project's real deterministic verification;
7. record the run using `dogfood/RUN_TEMPLATE.yaml`;
8. record human interventions and failures instead of hiding them;
9. update project state after accepted work;
10. review evidence periodically and only build BYOAI features that solve demonstrated friction.

See [`docs/QUICKSTART.md`](docs/QUICKSTART.md) for the complete Manual v0 workflow.

The draft `templates/project/byoai.yaml` manifest describes source-of-truth locations, expected verification, and human-approval boundaries. Its schema is provisional until dogfooding validates it.

## Product philosophy

- Bring your own AI.
- Repository is the source of truth.
- AI output is untrusted until verified.
- Deterministic checks beat self-confidence.
- Failures should become permanent guardrails.
- Humans decide intent, risk tolerance, and irreversible choices.
- Avoid rebuilding capabilities already provided well by existing AI platforms.
- Stay model-agnostic wherever practical.

## Source of truth

Project direction and operating rules live in this repository:

- [`docs/VISION.md`](docs/VISION.md)
- [`docs/MISSION.md`](docs/MISSION.md)
- [`docs/PRINCIPLES.md`](docs/PRINCIPLES.md)
- [`docs/PRODUCT.md`](docs/PRODUCT.md)
- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md)
- [`docs/ROADMAP.md`](docs/ROADMAP.md)
- [`docs/CURRENT_STATE.md`](docs/CURRENT_STATE.md)
- [`docs/DECISIONS.md`](docs/DECISIONS.md)
- [`docs/WORKFLOW.md`](docs/WORKFLOW.md)
- [`docs/DOGFOODING.md`](docs/DOGFOODING.md)
- [`AGENTS.md`](AGENTS.md)

Dogfood evidence lives under `dogfood/`; reusable target-project scaffolding lives under `templates/project/`.

## Current phase

BYOAI is currently in **Phase 0 — product discovery and operating-system design**.

The immediate goal is not to build a giant autonomous platform. The goal is to identify which problems remain unsolved when a solo builder uses existing AI tools to develop real software with minimal manual coding.

**Small is Dogfood Project #001.** Every repeated source of friction should either become a BYOAI feature, a reusable guardrail, or evidence that BYOAI does not need to own that capability.

## Working tagline

> **Your AI can code. BYOAI helps it engineer.**

## Status

Experimental and pre-alpha.
