---
name: idea-to-mvp
description: Turn rough product ideas or incomplete MVP documents into focused, build-ready specifications, stable decisions, traceable development tasks, and a reusable implementation prompt. Use when an app, AI tool, website, automation, or software idea needs a new MVP plan, a safe refinement, or resumed planning.
---

# Idea to MVP

Turn a rough product idea or incomplete planning package into four consistent, build-ready documents without starting full implementation.

## Select the Mode Safely

Inspect the working directory before writing:

- **Create:** None of the four deliverables exists. Build the package from the user's idea.
- **Refine:** Deliverables exist and the user asks to change the product or scope. Read all existing files first, preserve confirmed decisions, and update every affected file.
- **Resume:** Some deliverables are missing or incomplete and the user asks to continue planning. Preserve completed work and fill only the gaps required for a consistent package.

Never silently replace existing planning files. If files exist but the intended mode cannot be inferred, state what was found and ask one concise question before writing.

## Clarification Gate

Separate input into known facts, reasonable assumptions, and blocking questions. Ask only when an unknown has high impact on the target user, core problem, legal or safety boundary, or main workflow and no safe assumption is available. Record every material non-blocking assumption with confidence and impact in `PRODUCT.md`.

## Workflow

1. Extract the core problem, one primary target user, main scenario, desired outcome, core action, known constraints, and whether AI is necessary. Apply the clarification gate before asking anything.
2. Classify the AI role as `Essential`, `Useful`, `Optional`, or `Unnecessary`, with one concrete reason. Do not add an LLM when rules or ordinary software are sufficient.
3. Rewrite the idea as one precise MVP definition while preserving the user's direction.
4. Reduce V1 to one main problem, one main user flow, about 3–5 core features, and preferably no more than three primary pages. Separate `Core Features`, `Nice-to-Have`, and `Non-Goals`.
5. Rate scope risk as `LOW`, `MEDIUM`, or `HIGH`. Score product, engineering, and AI complexity from 1–5 and briefly justify each score.
6. Read [references/product-template.md](references/product-template.md) and create or safely update `PRODUCT.md`.
7. Read [references/decisions-template.md](references/decisions-template.md) and create or safely update `DECISIONS.md` with only decisions that constrain implementation.
8. Read [references/tasks-template.md](references/tasks-template.md) and create or safely update `TASKS.md`, ordered by dependency and covering every core feature.
9. Read [references/build-prompt-template.md](references/build-prompt-template.md) and create a self-contained `BUILD_PROMPT.md` for a new development session.
10. Read [references/validation-rules.md](references/validation-rules.md), validate all four documents, repair conflicts, and validate again before delivery.

Use [examples/weekend-planner.md](examples/weekend-planner.md), [examples/buying-assistant.md](examples/buying-assistant.md), or [examples/expense-splitter.md](examples/expense-splitter.md) only when a concrete example would clarify the expected level of scope, evidence, or non-AI behavior.

## Preserve Traceability

Assign stable IDs: `CF-01` for Core Features, `SC-01` for success criteria, `D-01` for decisions, and `T-01` for tasks. Do not renumber surviving items during Refine mode. Each Core Feature must map to at least one success criterion and one task; show the mapping in the `TASKS.md` coverage matrix.

## Scope Defaults

Unless one is essential to the user's core value, exclude accounts, payments, admin panels, social features, multi-agent systems, RAG, vector databases, MCP, real-time collaboration, complex permissions, microservices, and Kubernetes from V1. Keep an explicitly required capability and document its cost instead of silently removing it.

Recommend the simplest stack that satisfies the defined flow. Do not add infrastructure merely to demonstrate a technology.

## Implementation Boundary

Do not create product code by default. If the user explicitly asks to start building or create a starter project, first read `PRODUCT.md`, `DECISIONS.md`, and `TASKS.md`; then create only the smallest runnable skeleton for the first incomplete phase. Do not implement the full application or any non-goal.

## Delivery

Deliver `PRODUCT.md`, `DECISIONS.md`, `TASKS.md`, and `BUILD_PROMPT.md`, followed by the selected mode, a concise validation result, changed decisions, and material assumptions. The four files must agree on scope, AI role, stable IDs, technical choices, and task coverage.
