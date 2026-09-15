# Example — Weekend Planner

## Input

> 我想做一个 AI 应用，帮我决定周末去哪玩。

## Refined Idea

一个面向周末选择困难的城市年轻用户的轻量规划助手，根据城市、可用时段、预算、精力和天气偏好，一次生成 3 个现实可执行的本地活动方案。

## Scope Risk

**LOW** — 单一用户、单一生成流程、无需账号或数据库；唯一外部依赖是可选的天气数据与一次结构化 AI 生成。

## Complexity

- **产品复杂度:** 2 / 5 — 一个输入流程和一个结果页面。
- **工程复杂度:** 2 / 5 — 无登录、支付或持久化，只需简单接口。
- **AI 复杂度:** 2 / 5 — 单次调用并返回固定结构，不需要 Agent 或 RAG。

## Core Features

1. 收集城市、时间、预算、精力和室内/室外偏好。
2. 生成 3 个包含时间安排、预算区间和出行提示的方案。
3. 展示适合天气的标记与方案取舍。
4. 支持修改条件后重新生成。

## Non-Goals

- 用户账号和跨设备历史记录
- 地图导航、餐厅预订和门票购买
- 社交分享与多人协作
- 多 Agent、RAG 或向量数据库

## PRODUCT.md 示例

```markdown
# Product

## 产品名称
周末三选一（暂定）

## 一句话描述
帮助没有明确周末计划的城市年轻用户，用几个约束快速获得 3 个能实际执行的本地活动方案。

## 原始 Idea
我想做一个 AI 应用，帮我决定周末去哪玩。

## 优化后的 MVP 定义
一个根据城市、可用时段、预算、精力和天气偏好生成 3 个本地周末方案的轻量助手。

## Problem
用户想安排周末，但面对过多选择时难以把时间、预算和精力约束组合成可执行计划。

## Target User
没有明确周末计划且容易选择困难的城市年轻用户。

## Core Scenario
用户在周五晚上用一分钟输入限制，希望立刻得到周六或周日可执行的选择。

## Core User Flow
1. 输入城市、时间、预算、精力和天气偏好。
2. 提交并等待生成。
3. 比较 3 个结构一致的方案。
4. 修改条件并重新生成（如有需要）。

## Core Features
1. 约束输入表单。
2. 三方案结构化生成。
3. 带天气适配、预算和取舍的结果卡片。
4. 保留输入并重新生成。

## Nice-to-Have
- 将一个方案复制为文本。
- 使用实时天气自动填充天气条件。

## Non-Goals
- 登录、历史记录、预订、支付、地图导航和社交协作。
- 多 Agent、RAG、向量数据库和复杂推荐画像。

## AI Role
**Classification:** Useful

**Reason:** AI 擅长把多个软约束组合为多样化的自然语言方案，但核心体验也可用规则模板降级。

**Fallback:** 从按预算、时段和室内/室外标注的本地示例池中筛选 3 项。

## Important Assumptions
- V1 只面向一个城市的演示数据，不承诺商家信息实时准确。
- 用户无需保存结果到下一次会话。

## Recommended Tech Stack
- **Client:** 单页 React/Next.js 界面，支持表单和结果卡片。
- **Server:** 单个服务端生成端点，用于保护模型密钥。
- **Data:** 静态地点示例加会话内状态；无需数据库。
- **AI:** 一次生成调用，使用固定 JSON Schema 返回 3 个方案。
- **External services:** V1 可用用户选择的天气条件，不强依赖实时天气 API。

## Scope Risk
**Rating:** LOW

**Reasons:**
- 单一用户流程、4 个核心功能、无身份/支付/持久化。
- 一次有边界的 AI 调用。

**Recommended reduction:** No further reduction required for V1.

## Complexity
- **产品复杂度:** 2 / 5 — 两个主要页面状态。
- **工程复杂度:** 2 / 5 — 单端点且无数据库。
- **AI 复杂度:** 2 / 5 — 固定结构的单次生成。

## MVP Success Criteria
- 用户能在 60 秒内输入条件并获得 3 个完整方案。
- 每个方案都包含时段、预算、天气适配和至少一个取舍。
- 改变预算或精力后，结果能反映新的限制。

## Known Risks
- **地点信息失真:** V1 使用明确标注的演示地点并提示用户出发前核实。
- **输出格式漂移:** 服务端校验结构化响应，失败时允许重试。
```

## DECISIONS.md 示例

```markdown
# Product Decisions

## Decision 1 — V1 不做账号
决定：结果只保留在当前页面会话中。
原因：保存历史不是验证“快速得到可执行方案”的必要条件。
影响：刷新页面后结果可以丢失，不建设身份系统和数据库。

---

## Decision 2 — 固定生成三个方案
决定：每次返回且只返回 3 个结构一致的方案。
原因：给用户选择，同时避免新的选择过载。
影响：服务端 Schema 和结果 UI 固定为 3 项。

---

## Decision 3 — 天气由用户选择
决定：V1 让用户选择天气条件，不接实时天气 API。
原因：避免外部实时依赖，仍可验证天气适配价值。
影响：结果不得暗示天气数据为实时信息。

---

## Decision 4 — 使用结构化 AI 输出
决定：一次模型调用返回固定 JSON Schema。
原因：结果卡片需要稳定字段和可验证数量。
影响：接口必须校验响应并提供失败重试。

---

## Decision 5 — 地点为演示数据
决定：V1 只使用一个城市的小型地点列表作为生成上下文。
原因：减少地点准确性和检索系统的复杂度。
影响：不承诺广泛城市覆盖，不建设 RAG。
```

## TASKS.md 示例

```markdown
# Development Tasks

## Phase 1 — Setup
- [ ] Create the single-page app and one server endpoint; done when both start locally.
- [ ] Define input and three-plan response schemas; done when valid fixtures pass schema validation.

## Phase 2 — Core UI
- [ ] Build the constraint form; done when all five inputs can be submitted.
- [ ] Build three result cards; done when a fixture renders every required field.

## Phase 3 — Core Logic
- [ ] Implement the structured generation endpoint; done when it returns exactly three valid plans.
- [ ] Connect form submission to the endpoint; done when inputs produce rendered results.
- [ ] Preserve inputs for regeneration; done when one constraint can be edited without re-entering the rest.

## Phase 4 — Product States
- [ ] Add input validation and loading state; done when empty input is blocked and duplicate submissions are prevented.
- [ ] Add generation failure and retry state; done when an invalid response shows a recoverable error.

## Phase 5 — Polish
- [ ] Make form and cards keyboard-usable and responsive; done when the core flow works at mobile width without horizontal scrolling.

## Phase 6 — Demo
- [ ] Add two representative input fixtures; done when low-budget and rainy-day scenarios both render valid plans.
- [ ] Run the end-to-end core flow; done when every PRODUCT success criterion is observed.
```

## BUILD_PROMPT.md 示例

The generated prompt instructs a new session to read `PRODUCT.md`, `DECISIONS.md`, and `TASKS.md`, begin with the first unchecked Phase 1 task, use only a single structured generation endpoint and session state, avoid accounts/databases/RAG, run the app after the phase, and update only verified task checkboxes.

