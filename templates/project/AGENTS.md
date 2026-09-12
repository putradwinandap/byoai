# AGENTS.md

This repository is developed with AI assistance under the BYOAI operating model.

## Mandatory reading

Before meaningful work, read:

1. `docs/CURRENT_STATE.md`
2. the active issue/task
3. relevant `docs/PRODUCT.md`
4. relevant `docs/ARCHITECTURE.md`
5. `docs/DECISIONS.md`
6. `docs/WORKFLOW.md`
7. `byoai.yaml`

Repository state is authoritative over conversational memory.

## Rules

- Human owns product intent and consequential decisions.
- Keep work bounded to the active issue.
- Inspect before editing.
- Treat AI-generated changes as untrusted until verified.
- Prefer deterministic verification to AI self-assessment.
- Never claim a check passed unless it was actually executed.
- Do not weaken tests/security to make work pass.
- Investigate root causes instead of blindly rerunning CI.
- Turn recurring preventable failures into earlier guardrails where practical.
- Update durable source of truth when project reality changes.
- Never commit secrets.

## Completion report

Report what changed, what was verified, what was not verified, remaining risks/blockers, and whether source-of-truth state changed.
