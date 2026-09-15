---
name: idea-to-mvp
description: Turn rough or vague product ideas into focused, build-ready MVP specifications, product decisions, development tasks, and a reusable implementation prompt. Use when a user has an app, AI tool, website, automation, or software idea but has not yet defined a clear MVP scope or development plan.
---

# Idea to MVP

Turn a rough product idea into four consistent, build-ready documents without starting full implementation.

## Workflow

1. Extract the core problem, one primary target user, main scenario, desired outcome, core action, known constraints, and whether AI is necessary. Ask only when a missing answer would materially change the product direction; otherwise make a reasonable assumption and record it.
2. Classify the AI role as `Essential`, `Useful`, `Optional`, or `Unnecessary`, with one concrete reason. Do not add an LLM when rules or ordinary software are sufficient.
3. Rewrite the idea as one precise MVP definition while preserving the user's direction.
4. Reduce V1 to one main problem, one main user flow, about 3–5 core features, and preferably no more than three primary pages. Separate `Core Features`, `Nice-to-Have`, and `Non-Goals`.
5. Rate scope risk as `LOW`, `MEDIUM`, or `HIGH`. Score product, engineering, and AI complexity from 1–5 and briefly justify each score.
6. Read [references/product-template.md](references/product-template.md) and create `PRODUCT.md`.
7. Read [references/decisions-template.md](references/decisions-template.md) and create `DECISIONS.md` with only decisions that constrain implementation.
8. Read [references/tasks-template.md](references/tasks-template.md) and create `TASKS.md`, ordered by dependency and covering every core feature.
9. Read [references/build-prompt-template.md](references/build-prompt-template.md) and create a self-contained `BUILD_PROMPT.md` for a new development session.
10. Read [references/validation-rules.md](references/validation-rules.md), validate all four documents, repair conflicts, and validate again before delivery.

Use [examples/weekend-planner.md](examples/weekend-planner.md) or [examples/buying-assistant.md](examples/buying-assistant.md) only when a concrete example would clarify the expected level of scope or detail.

## Scope Defaults

Unless one is essential to the user's core value, exclude accounts, payments, admin panels, social features, multi-agent systems, RAG, vector databases, MCP, real-time collaboration, complex permissions, microservices, and Kubernetes from V1. Keep an explicitly required capability and document its cost instead of silently removing it.

Recommend the simplest stack that satisfies the defined flow. Do not add infrastructure merely to demonstrate a technology.

## Implementation Boundary

Do not create product code by default. If the user explicitly asks to start building or create a starter project, first read `PRODUCT.md`, `DECISIONS.md`, and `TASKS.md`; then create only the smallest runnable skeleton for the first incomplete phase. Do not implement the full application or any non-goal.

## Delivery

Deliver `PRODUCT.md`, `DECISIONS.md`, `TASKS.md`, and `BUILD_PROMPT.md`, followed by a concise validation result and any material assumptions. The four files must agree on scope, AI role, technical choices, and task coverage.
