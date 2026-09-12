# Vision

## Long-term vision

Make autonomous software engineering accessible to people who already have access to a capable general-purpose AI.

BYOAI should make it possible for a solo builder to provide product intent while an AI-assisted engineering system handles an increasingly large share of planning, implementation, verification, delivery, and project continuity.

## The future we want

A developer should not need subscriptions to multiple specialized AI software platforms just to obtain a disciplined AI-native workflow.

They should be able to bring the AI they already use — whether ChatGPT/Codex, Claude, Gemini, a local model, or something that does not exist yet — and connect it to a reusable engineering control plane.

The resulting system should be:

- model-agnostic;
- repository-native;
- verifiable;
- failure-aware;
- progressively more autonomous;
- affordable for individual builders;
- replaceable at the AI-provider layer;
- explicit about when human judgment is still required.

## North-star experience

The long-term interaction should approach:

```text
Human: "Build this product / implement this outcome."

BYOAI:
✓ understands current project state
✓ plans bounded work
✓ selects/uses an available AI worker
✓ implements the change
✓ verifies behavior
✓ investigates failures
✓ records reusable lessons
✓ creates a reviewable change
✓ ships when policy allows
✓ updates project state
```

The human remains responsible for product intent and consequential decisions, but manual coordination and repetitive engineering work trend toward zero.

## What BYOAI is not

BYOAI is not trying to create the smartest coding model, replace GitHub, replace CI, replace deployment platforms, or recreate every feature offered by mature coding agents.

BYOAI wins by making those existing capabilities work together as a reliable engineering system.
