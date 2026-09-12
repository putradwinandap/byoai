# AI-Native Development Workflow

This workflow governs development of BYOAI itself.

## Core loop

```text
Source of truth
    ↓
Issue
    ↓
Read current state + relevant decisions
    ↓
Plan bounded change
    ↓
Implement
    ↓
Local verification
    ↓
PR
    ↓
CI / review
    ↓
Merge
    ↓
Update current state / lessons
```

## Before starting work

An AI agent must:

1. Read `AGENTS.md`.
2. Read `docs/CURRENT_STATE.md`.
3. Read the issue completely.
4. Inspect relevant source and documentation.
5. Check `docs/DECISIONS.md` and architecture for constraints.
6. Confirm that the requested work is not already complete.
7. Identify verification requirements before editing.

## Issue discipline

Implementation work should normally have a GitHub issue containing:

- problem/context;
- desired outcome;
- scope;
- non-goals where relevant;
- acceptance criteria;
- verification expectations.

Prefer vertical, independently verifiable slices over large horizontal rewrites.

## Branch and PR discipline

Unless explicitly agreed otherwise:

- do not implement meaningful features directly on `main`;
- use a focused branch;
- keep the change bounded to the issue;
- create a PR;
- inspect CI before merge;
- merge only when acceptance criteria and required checks are satisfied.

## Failure protocol

A failed check is not merely an obstacle to bypass.

For each meaningful failure:

1. identify the root cause;
2. fix the immediate problem;
3. determine whether the failure class is likely to recur;
4. if recurring and preventable, add the cheapest reliable earlier guardrail;
5. record a durable lesson when it affects future work;
6. avoid blindly rerunning CI when the cause has not changed.

This is especially important for conserving CI resources and improving the factory over time.

## Source-of-truth updates

Update `CURRENT_STATE.md` when a merged change materially alters:

- current phase;
- completed milestones;
- immediate next steps;
- unresolved blockers;
- validated/rejected hypotheses.

Update `DECISIONS.md` when a durable decision changes.

Update architecture/product docs only when reality or an accepted decision changes; do not rewrite them after every issue.

## Definition of done

An issue is not done merely because code exists.

At minimum:

- acceptance criteria are satisfied;
- relevant deterministic verification passes;
- regressions are covered where appropriate;
- security implications are considered;
- docs/state are updated when needed;
- CI is green where CI exists;
- the resulting state is understandable by a fresh agent.

## Human escalation

Escalate rather than guess when work involves:

- unclear product intent with materially different outcomes;
- destructive or irreversible operations;
- secrets or credentials;
- major architecture changes not covered by an accepted decision;
- significant security tradeoffs;
- cost-bearing external actions;
- insufficient evidence to safely merge or deploy.
