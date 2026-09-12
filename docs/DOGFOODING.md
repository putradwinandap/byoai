# BYOAI Dogfooding Protocol

## Purpose

BYOAI must be built from evidence rather than assumptions. Dogfooding measures what happens when a real product is developed primarily through an existing AI worker while the human avoids manual source-code work.

**Dogfood Project #001: Small.**

Small is intentionally the first experiment because it can be observed from an early product state through MVP development. The human defines intent and makes consequential product decisions; AI performs as much engineering work as possible. Every meaningful human intervention becomes evidence.

## Core experiment rule

> Human owns intent. AI performs engineering. BYOAI records why the human still had to intervene.

Do not artificially prevent necessary human intervention. Record it accurately instead. The goal is measurement, not a staged autonomy demo.

## Unit of observation

One **run** represents one bounded engineering task, normally one GitHub issue or an independently verifiable slice of an issue. Each run receives an ID such as `SMALL-0001` and one run log under `dogfood/runs/`.

## Procedure

### Before the run

1. Define a bounded task and acceptance criteria.
2. Record the starting repository/ref and AI worker.
3. Record the context supplied to the AI.
4. Record required verification before implementation begins.
5. Do not manually edit source code to make the run easier.

### During the run

Record meaningful events: clarification requests, human corrections/decisions, AI retries, failed local checks, failed CI, incorrect assumptions from missing/stale context, permission/tool limitations, verification gaps, and work the human had to perform manually.

Minor conversational steering that does not change engineering execution does not need to be counted as intervention.

### After the run

1. Record the outcome.
2. Classify every human intervention and meaningful failure.
3. Record verification evidence actually executed.
4. Identify root causes rather than only symptoms.
5. Decide whether the observation reveals a candidate BYOAI capability.
6. Prefer the cheapest reliable guardrail over adding another AI agent.

## Human intervention classes

Use one primary class per intervention:

- `product-decision` — legitimate human judgment about intent/tradeoffs.
- `missing-context` — durable/relevant project knowledge could have been supplied automatically.
- `incorrect-context` — supplied knowledge was stale, conflicting, or wrong.
- `orchestration` — human coordinated steps/tools that could plausibly be automated.
- `verification` — human determined correctness because evidence/checks were insufficient.
- `tool-capability` — AI/tool could not perform a required action despite adequate context.
- `permission-safety` — human approval was appropriate for sensitive/destructive/irreversible/cost-bearing work.
- `recovery` — human recovered a run after an agent/tool failure.
- `other` — explain why no existing class fits.

`product-decision` and `permission-safety` are not automatically defects. BYOAI reduces unnecessary intervention, not legitimate human authority.

## Failure classes

- `implementation-defect`
- `test-defect`
- `format-static-defect`
- `security-defect`
- `context-defect`
- `environment-infrastructure`
- `workflow-configuration`
- `tool-provider`
- `flaky-nondeterministic`
- `requirements-ambiguity`
- `other`

For each failure record root cause, detection point, preventability, recurrence likelihood, and whether a cheaper/earlier guardrail exists.

## Candidate BYOAI capability test

An observation becomes a feature candidate when most are true:

1. It caused meaningful human effort, delay, cost, or risk.
2. It is reusable beyond one highly specific incident.
3. Existing tools do not already solve it adequately with reasonable configuration.
4. BYOAI can address it at the control-plane/repository/workflow layer.
5. Improvement can be measured with observable evidence.

Repeated preventable failures are particularly strong candidates. Do not create a feature merely because an AI worker made one mistake; first consider better context, prompting, existing tooling, deterministic checks, or normal project configuration.

## Baseline metrics

Metrics are initially calculated manually from run logs.

- **Human intervention rate:** runs requiring avoidable human intervention / total runs. Track legitimate product/safety interventions separately.
- **Autonomous completion rate:** runs completed without avoidable human intervention / total runs.
- **First-pass verification rate:** runs passing all required verification on first attempt / total completed runs.
- **Repeated preventable failure rate:** preventable failures belonging to a previously observed failure class / total preventable failures.
- **CI efficiency:** CI runs per completed task, including reruns caused by defects that could have been caught locally.
- **Retry count:** AI implementation/recovery attempts per run.
- **Cycle time:** approximate elapsed time from bounded task start to verified completion.
- **Escaped defect rate:** defects discovered after a run was considered verified.
- **Candidate yield:** credible BYOAI capability candidates revealed. This is a discovery metric, not something to maximize artificially.

## Distinguishing the real problem

Before proposing BYOAI functionality, classify friction as:

1. **AI capability limitation** — worker understood the task but could not reliably perform it.
2. **Context problem** — worker lacked, received stale, or received excessive/irrelevant context.
3. **Verification problem** — correctness could not be established reliably.
4. **Orchestration problem** — human moved information/actions between otherwise capable tools.
5. **Existing-tool configuration problem** — mature tooling already solves it; integrate/configure instead of rebuilding.
6. **BYOAI candidate** — a reusable missing control-plane mechanism remains.

## Small experiment policy

For Dogfood Project #001:

- Small is the product under development.
- The user remains product owner.
- AI performs source-code implementation whenever tooling permits.
- Manual source-code editing by the user counts as significant intervention and must be logged with its cause.
- Genuine product clarification does not count as avoidable intervention.
- Normal engineering quality standards remain in force; never weaken tests to improve autonomy metrics.
- BYOAI should not gain a feature until Small or another real run provides evidence for it, except minimal experiment infrastructure.

## Review cadence

Review evidence after approximately every 5 completed runs, or immediately when the same preventable failure class appears twice.

At review time: aggregate metrics; identify repeated intervention/failure classes; check whether existing tools already solve them; propose the smallest BYOAI improvement; predict which metric should improve; implement only when justified; compare later runs against baseline.

## Success of Phase 0

Phase 0 succeeds when evidence reveals at least one meaningful recurring gap that BYOAI can reduce measurably without rebuilding a mature capability.

Phase 0 can also succeed by falsifying the thesis. If existing AI + repository conventions + normal engineering tools already remove the relevant friction, BYOAI should change direction rather than manufacture a product need.
