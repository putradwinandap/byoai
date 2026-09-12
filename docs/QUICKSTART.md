# BYOAI Manual v0 Quickstart

BYOAI is currently a repository protocol and engineering methodology, not yet an installable autonomous runtime.

This quickstart describes how to use **BYOAI Manual v0** with an AI you already have.

## 1. Choose a target project

Use a real software project. BYOAI itself is the control-plane project; the target project is where engineering work happens.

Dogfood Project #001 is **Small**.

## 2. Bootstrap the target repository

Copy/adapt the files under `templates/project/` into the target repository.

At minimum the target should have:

```text
AGENTS.md
docs/
  VISION.md
  PRODUCT.md
  ARCHITECTURE.md
  CURRENT_STATE.md
  DECISIONS.md
  WORKFLOW.md
byoai.yaml
```

Replace all template placeholders with project reality. Do not leave invented architecture decisions in place.

## 3. Define bounded work

Create a GitHub issue with a clear outcome, scope, acceptance criteria, and verification expectations.

One BYOAI dogfood run should normally map to one bounded issue or independently verifiable slice.

## 4. Start a run

Copy `dogfood/RUN_TEMPLATE.yaml` to a new file under `dogfood/runs/` in the BYOAI repository.

For Small, the first real run is:

```text
dogfood/runs/SMALL-0001.yaml
```

Record the target repository, issue, starting ref, AI worker, context supplied, and verification plan before implementation.

## 5. Give the AI the operating contract

The AI working on the target repository should read, in order:

1. target `AGENTS.md`;
2. target `docs/CURRENT_STATE.md`;
3. active issue;
4. relevant product/architecture/decision docs;
5. target `byoai.yaml`;
6. relevant source code.

A useful human instruction is simply:

> Read the repository source of truth and active issue first. Work according to AGENTS.md. Implement the bounded issue, run the required verification, and do not claim checks passed unless they were actually executed.

The exact wording is not part of the protocol; repository state is authoritative.

## 6. Let AI perform engineering

The experiment aims for AI to perform source-code implementation whenever tooling permits.

Do not manually fix code merely to preserve the appearance of autonomy. If human intervention becomes necessary, perform it safely and record why.

## 7. Verify before trust

Use the target project's actual deterministic checks. Typical examples include formatting, linting, unit tests, integration tests, build, security checks, and E2E tests.

The checks declared in `byoai.yaml` describe the project's expected verification contract; they do not replace the actual tools.

## 8. Complete the run log

After the task, record:

- outcome;
- human interventions;
- failures and root causes;
- actual verification evidence;
- AI attempts;
- CI usage;
- approximate cycle time;
- whether the user manually edited source code;
- candidate BYOAI capability, if any.

Use `docs/DOGFOODING.md` for classification rules.

## 9. Update target state

If the implementation materially changed project reality, update the target's `docs/CURRENT_STATE.md` and any affected durable decisions.

A fresh AI session should be able to continue without reconstructing project history from chat.

## 10. Review evidence periodically

After approximately five real runs, or when the same preventable failure class appears twice:

1. update `dogfood/METRICS.md`;
2. inspect repeated friction;
3. check whether mature tools already solve it;
4. propose the smallest reusable BYOAI improvement;
5. predict which metric should improve;
6. only then implement a BYOAI feature.

## Current manual loop

```text
Human intent
    ↓
Target source of truth
    ↓
Bounded GitHub issue
    ↓
AI worker
    ↓
Candidate implementation
    ↓
Deterministic verification
    ↓
PR / accepted change
    ↓
Run log + project state
    ↓
Evidence review
    ↺
```

Future CLI commands such as `byoai init`, `byoai doctor`, and `byoai run` should automate this proven manual workflow rather than invent a different one.