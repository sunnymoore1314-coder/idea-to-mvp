# DECISIONS.md Template

Record only choices that a later implementer might otherwise revisit or interpret differently. Aim for about 5–10 decisions, but use fewer when fewer matter.

```markdown
# Product Decisions

## Decision D-01 — <Short decision title>

状态：
Confirmed | Assumed

决定：
<A specific choice, stated unambiguously.>

原因：
<Why this choice supports the MVP goal or constraint.>

影响：
<What implementation, data, UX, or future option this constrains.>

---

## Decision D-02 — <Short decision title>

状态：
Confirmed | Assumed

决定：
...

原因：
...

影响：
...
```

Keep decision IDs stable in Refine mode. When a decision changes, update it in place and add `变更：<what changed and why>` below its impact instead of creating a contradictory decision.

Good decision topics include authentication, persistence, source of truth, external APIs, AI output contract, failure behavior, privacy boundary, platform, and explicit scope exclusions.

Do not record tautologies, generic quality goals, task instructions, or features already obvious from their names. Every decision must agree with `PRODUCT.md`; if it changes a core feature, update the product definition first.
