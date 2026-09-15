# PRODUCT.md Template

Use this template to turn the user's idea into a compact implementation contract. Replace every instruction with project-specific content; omit no section unless it is genuinely inapplicable.

```markdown
# Product

## 产品名称

<Short working name. Mark it as provisional when inferred.>

## 一句话描述

<Who the product helps, what core action it enables, and what outcome it produces.>

## 原始 Idea

<Preserve or faithfully paraphrase the user's original idea.>

## 优化后的 MVP 定义

<One sentence defining one primary user, one problem, one core flow, and a bounded outcome.>

## Problem

<The concrete problem, its context, and why the current alternative is insufficient. Avoid market analysis.>

## Target User

<One primary user type. Mention secondary users only when the core flow cannot work without them.>

## Core Scenario

<The single most important situation in which the user reaches for the product.>

## Core User Flow

1. <Entry/input>
2. <Core processing or decision>
3. <Useful result>
4. <Optional final action only if essential>

## Core Features

1. <Feature required by the core flow>
2. <Feature required by the core flow>
3. <Feature required by the core flow>

Keep this list at roughly 3–5 items. Each feature must map to the core flow and later to one or more tasks.

## Nice-to-Have

- <Useful but unnecessary for validating the core experience>

## Non-Goals

- <Explicitly excluded feature, audience, workflow, or infrastructure choice>

## AI Role

**Classification:** Essential | Useful | Optional | Unnecessary

**Reason:** <Why AI is or is not justified and exactly where it appears in the flow.>

**Fallback:** <Rule-based or manual alternative when practical; write “Not required” when AI is unnecessary.>

## Important Assumptions

- <Material assumption made because the user did not specify it>
- <Constraint that affects scope or implementation>

## Recommended Tech Stack

- **Client:** <Simplest suitable UI technology>
- **Server:** <Only when needed>
- **Data:** <Local/session storage before a database when sufficient>
- **AI:** <Provider-neutral capability and output contract, or “None”>
- **External services:** <Only services required by the core flow>

For each non-obvious component, include a short reason. Do not turn this section into an architecture document.

## Scope Risk

**Rating:** LOW | MEDIUM | HIGH

**Reasons:**
- <Evidence such as number of flows, integrations, identity, real-time data, payment, or AI workflow complexity>

**Recommended reduction:** <Required when MEDIUM or HIGH; otherwise write “No further reduction required for V1.”>

## Complexity

- **产品复杂度:** <1–5> / 5 — <brief reason>
- **工程复杂度:** <1–5> / 5 — <brief reason>
- **AI 复杂度:** <1–5> / 5 — <brief reason>

## MVP Success Criteria

- <Observable end-to-end outcome>
- <Quality or reliability threshold appropriate for a demo/MVP>
- <Evidence that the core problem was reduced>

Avoid unsupported business metrics. Prefer criteria that can be checked during a small pilot or demo.

## Known Risks

- **<Risk>:** <Impact and a proportionate V1 mitigation>
```

## Quality Bar

- Preserve the user's intent while making assumptions visible.
- Define one primary user, one problem, and one dominant flow.
- Make every core feature necessary to the success criteria.
- Keep nice-to-have items out of the development task baseline.
- Treat non-goals as hard V1 boundaries unless the user later changes them.
- Align the AI classification with the actual proposed implementation.

