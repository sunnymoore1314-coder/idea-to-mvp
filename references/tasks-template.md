# TASKS.md Template

Translate the accepted MVP into ordered, verifiable implementation work. Start every task with an action verb, keep it independently executable where practical, and include an observable completion check.

```markdown
# Development Tasks

## Phase 1 — Setup

- [ ] **T-01** `[FOUNDATION]` Create <minimal project structure/configuration>; done when <observable check>.
- [ ] **T-02** `[CF-01]` Define <shared types/schema/contracts>; done when <observable check>.

## Phase 2 — Core UI

- [ ] **T-03** `[CF-01]` Build <input or primary interface>; done when <observable check>.
- [ ] **T-04** `[CF-02]` Render <primary result>; done when <observable check>.

## Phase 3 — Core Logic

- [ ] **T-05** `[CF-02]` Implement <core transformation/decision/API>; done when <observable check>.
- [ ] **T-06** `[CF-01][CF-02]` Connect <input> to <result>; done when <observable check>.

## Phase 4 — Product States

- [ ] **T-07** `[STATE]` Add <validation/loading/empty/error state>; done when <observable check>.
- [ ] **T-08** `[STATE]` Handle <expected failure>; done when <observable check>.

## Phase 5 — Polish

- [ ] **T-09** `[QUALITY]` Improve <specific accessibility/responsiveness/usability property>; done when <observable check>.

## Phase 6 — Demo

- [ ] **T-10** `[SC-01]` Add <small representative demo fixture or scenario>; done when <observable check>.
- [ ] **T-11** `[SC-01][SC-02]` Run <targeted validation>; done when <observable check>.

## Coverage Matrix

| Core Feature | Task IDs | Success Criteria |
| --- | --- | --- |
| CF-01 | T-02, T-03, T-06 | SC-01 |
| CF-02 | T-04, T-05, T-06 | SC-01, SC-02 |
| CF-03 | <task IDs> | <success criterion IDs> |
```

## Task Rules

- Order tasks by dependency and keep the project runnable at every phase boundary.
- Cover every `Core Feature` and every required state from `PRODUCT.md`.
- Preserve existing `T-*` IDs in Refine mode; assign new IDs only to new tasks.
- Use `[FOUNDATION]`, `[STATE]`, or `[QUALITY]` only for necessary work that does not implement one Core Feature directly.
- Include every `CF-*` ID exactly once in the coverage matrix with at least one task and one success criterion.
- Do not schedule `Nice-to-Have` or `Non-Goals` as V1 work.
- Reflect all architectural constraints in `DECISIONS.md`.
- Use concrete verbs such as Create, Define, Implement, Connect, Validate, Render, Handle, or Test.
- Replace vague tasks such as “Improve UX” with the exact interface/state and a completion condition.
- Do not add deployment, analytics, authentication, payment, or elaborate test infrastructure unless the product documents require it.
