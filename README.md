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
- [`AGENTS.md`](AGENTS.md)

## Current phase

BYOAI is currently in **Phase 0 — product discovery and operating-system design**.

The immediate goal is not to build a giant autonomous platform. The goal is to identify which problems remain unsolved when a solo builder uses existing AI tools to develop real software with minimal manual coding.

Real projects should be used as dogfooding environments. Every repeated source of friction should either become a BYOAI feature, a reusable guardrail, or evidence that BYOAI does not need to own that capability.

## Working tagline

> **Your AI can code. BYOAI helps it engineer.**

## Status

Experimental and pre-alpha.
