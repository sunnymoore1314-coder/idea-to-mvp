# TASKS.md Template

Translate the accepted MVP into ordered, verifiable implementation work. Start every task with an action verb, keep it independently executable where practical, and include an observable completion check.

```markdown
# Development Tasks

## Phase 1 — Setup

- [ ] Create <minimal project structure/configuration>; done when <observable check>.
- [ ] Define <shared types/schema/contracts>; done when <observable check>.

## Phase 2 — Core UI

- [ ] Build <input or primary interface>; done when <observable check>.
- [ ] Render <primary result>; done when <observable check>.

## Phase 3 — Core Logic

- [ ] Implement <core transformation/decision/API>; done when <observable check>.
- [ ] Connect <input> to <result>; done when <observable check>.

## Phase 4 — Product States

- [ ] Add <validation/loading/empty/error state>; done when <observable check>.
- [ ] Handle <expected failure>; done when <observable check>.

## Phase 5 — Polish

- [ ] Improve <specific accessibility/responsiveness/usability property>; done when <observable check>.

## Phase 6 — Demo

- [ ] Add <small representative demo fixture or scenario>; done when <observable check>.
- [ ] Run <targeted validation>; done when <observable check>.
```

## Task Rules

- Order tasks by dependency and keep the project runnable at every phase boundary.
- Cover every `Core Feature` and every required state from `PRODUCT.md`.
- Do not schedule `Nice-to-Have` or `Non-Goals` as V1 work.
- Reflect all architectural constraints in `DECISIONS.md`.
- Use concrete verbs such as Create, Define, Implement, Connect, Validate, Render, Handle, or Test.
- Replace vague tasks such as “Improve UX” with the exact interface/state and a completion condition.
- Do not add deployment, analytics, authentication, payment, or elaborate test infrastructure unless the product documents require it.

