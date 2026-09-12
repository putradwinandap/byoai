# Principles

These principles are constraints, not marketing slogans. Future agents should use them when evaluating architecture and product decisions.

## 1. Bring Your Own AI

The AI provider is a dependency, not the product identity. Avoid hard coupling to one model or vendor unless an integration genuinely requires it.

## 2. Repository as source of truth

Important project state must survive chat sessions, agent replacements, and model changes. Durable context belongs in version-controlled artifacts.

## 3. AI output starts untrusted

A model saying that its work is correct is not evidence that its work is correct. Verification should prefer deterministic evidence whenever possible.

## 4. Verification before autonomy

Higher autonomy is earned by stronger verification. Auto-merge and auto-deploy must be consequences of evidence and policy, not goals by themselves.

## 5. Fail once, learn permanently

Repeated avoidable failures are system defects. When a failure reveals a reusable lesson, encode it as a test, validation, rule, check, fixture, or documented constraint.

## 6. Do not rebuild mature tools without a reason

GitHub can manage Git collaboration. Existing agents can write code. CI systems can execute checks. Deployment platforms can deploy. BYOAI should orchestrate and govern them unless owning a capability creates clear leverage.

## 7. Humans own intent

AI can propose product and architecture decisions, but humans define goals, acceptable risk, irreversible choices, and value judgments.

## 8. Bounded autonomy

Every autonomous action should have explicit scope, permissions, retry limits, and escalation behavior.

## 9. Evidence over agent count

A workflow with two well-verified AI steps is preferable to a theatrical swarm of twenty agents. Agent count is not a success metric.

## 10. Progressive enhancement

BYOAI should be useful with a simple setup and gain capability as users connect more tools. A basic GitHub + AI subscription workflow should remain a first-class use case.

## 11. Dogfood before abstraction

Do not invent infrastructure because it sounds useful. Observe friction in real AI-native development, solve it, then generalize it.

## 12. Measure the factory

Track metrics such as human intervention rate, repeated failure rate, verification pass rate, cost per completed task, cycle time, rollback rate, and escaped defects where practical.
