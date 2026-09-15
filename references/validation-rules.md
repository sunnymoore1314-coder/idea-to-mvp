# MVP Validation Rules

Validate logic across `PRODUCT.md`, `DECISIONS.md`, `TASKS.md`, and `BUILD_PROMPT.md`. This is not a wording or style review.

## 1. Scope Consistency

- There is one primary target user and one core problem.
- There is one dominant end-to-end user flow.
- Core Features are normally limited to 3–5 and each is required by that flow.
- Nice-to-Have items are not described elsewhere as required for V1.
- Non-Goals do not appear as planned work or required architecture.
- A MEDIUM or HIGH scope risk includes a concrete reduction recommendation.

## 2. Feature and Task Consistency

- Every Core Feature maps to at least one actionable task.
- Every task supports a Core Feature, a necessary product state, setup, verification, or demo.
- Tasks use concrete actions, are dependency-ordered, and include a completion condition.
- No task silently introduces a new user type, flow, integration, page, or persistence requirement.

Create a temporary coverage mapping while validating:

```text
Core Feature -> Task(s) -> Success Criterion
```

Do not add this mapping to the deliverables unless it helps explain a conflict.

## 3. Decision Consistency

- Each decision affects implementation and includes a decision, reason, and impact.
- Decisions agree with the Product's scope, stack, AI role, and non-goals.
- Technical choices referenced by tasks are either obvious minimal setup or fixed in Decisions.
- No decision adds a feature merely because the chosen technology supports it.

## 4. AI Necessity

- The AI classification is one of `Essential`, `Useful`, `Optional`, or `Unnecessary`.
- The reason identifies the exact product step that benefits from AI.
- `Unnecessary` projects contain no LLM tasks or AI infrastructure.
- `Optional` projects remain useful without AI.
- Simple generation/classification uses a bounded call and stable output contract rather than an agent loop unless the product requires iteration or tool use.

## 5. Technical Proportionality

- The stack is the smallest one that supports the core flow.
- Authentication, payment, databases, queues, real-time systems, RAG, vector stores, MCP, multi-agent designs, microservices, and orchestration appear only when core to the product.
- The complexity scores and scope-risk rating reflect actual dependencies and external services.
- The plan includes failure states for required APIs or AI calls without inventing excessive infrastructure.

## 6. Build Prompt Independence

- It names every file a new session must read.
- It identifies the first unfinished task/phase as the starting point.
- It preserves Core Features, Non-Goals, decisions, and AI boundaries.
- It requires runnable checks, error repair, task-status updates, and a completion summary.
- It contains no unresolved placeholders or reliance on the original chat.

## Required Review Questions

1. Is there only one primary target user?
2. Is there only one core problem?
3. Is the core user flow explicit?
4. Are there roughly 3–5 Core Features?
5. Do tasks cover every Core Feature?
6. Do tasks include any Non-Goal?
7. Do Decisions conflict with Product?
8. Can Build Prompt be used in a new session?
9. Is the recommended stack larger than the MVP requires?
10. Does the AI role match the implemented functionality?

## Repair Loop

1. List each conflict with the files and concepts involved.
2. Resolve it using this priority: explicit user requirement, refined MVP definition, Core Features and Non-Goals, Decisions, Tasks, Build Prompt.
3. Prefer removing unnecessary scope over adding new features or infrastructure.
4. Update every affected file, not only the first file where the conflict appeared.
5. Re-run all six validation sections. Deliver only after no blocking conflicts remain.

