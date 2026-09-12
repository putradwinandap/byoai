# Engineering Workflow

## Core loop

```text
source of truth → issue → plan → implement → local verification → PR → CI/review → merge → update state
```

## Before work

1. Read `AGENTS.md` and `docs/CURRENT_STATE.md`.
2. Read the active issue completely.
3. Inspect relevant code and durable decisions.
4. Identify verification requirements before editing.

## Issue requirements

A bounded implementation issue should define problem/context, desired outcome, scope, acceptance criteria, and verification expectations.

## Failure protocol

When a meaningful failure occurs:

1. identify root cause;
2. fix the immediate defect;
3. decide whether it can recur;
4. add the cheapest reliable earlier guardrail when appropriate;
5. avoid rerunning CI without changing the underlying cause.

## Definition of done

Work is done when acceptance criteria are satisfied, required verification actually passes, regressions are covered where appropriate, security implications are considered, and durable state/docs are updated when reality changed.
