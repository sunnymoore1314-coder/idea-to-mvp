# Example — Buying Assistant

## Input

> 我想做一个 AI 应用，帮我判断一个商品值不值得买。

## Refined Idea

一个面向考虑购买单件消费电子产品的普通消费者的决策助手，根据价格、使用需求、关键参数和用户粘贴的评价摘要，输出“值得买 / 有条件值得买 / 不建议买”及可核查理由。

## Scope Risk

**MEDIUM** — 判断需要多种输入与清晰证据边界，但 V1 通过用户粘贴资料、限定消费电子品类并取消实时比价，将外部依赖降为零。

## Complexity

- **产品复杂度:** 3 / 5 — 需要把主观需求转成明确判断维度。
- **工程复杂度:** 2 / 5 — 表单、一次分析端点和结果页，无爬虫或数据库。
- **AI 复杂度:** 3 / 5 — 需结构化提取、加权分析和引用用户输入，但不需要 RAG 或 Agent。

## Core Features

1. 收集商品信息、价格、使用需求和评价文本。
2. 提取关键优点、缺点、风险与信息缺口。
3. 输出三级购买结论、理由和适用条件。
4. 区分用户提供的事实与模型推断。

## Non-Goals

- 全网抓取、实时比价和自动读取电商页面
- 联盟链接、支付和购物车
- 跨品类专业鉴定或投资建议
- 用户账号、推荐画像、RAG 和多 Agent

## PRODUCT.md 示例

```markdown
# Product

## 产品名称
值不值（暂定）

## 一句话描述
帮助考虑购买单件消费电子产品的用户，把商品资料和自身需求转成有证据边界的购买建议。

## 原始 Idea
我想做一个 AI 应用，帮我判断一个商品值不值得买。

## 优化后的 MVP 定义
一个分析用户粘贴的消费电子商品资料、价格、需求和评价摘要，并输出三级购买结论与可核查理由的工具。

## Problem
用户面对参数和评价时难以区分与自身需求相关的信号、营销描述和未知信息，容易凭单一观点做决定。

## Target User
正在考虑购买一件消费电子产品、但不擅长整理参数和评价的普通消费者。

## Core Scenario
用户在下单前粘贴商品信息和若干评价，希望判断该价格下是否符合自己的主要用途。

## Core User Flow
1. 输入商品、价格、主要用途、关键偏好和评价文本。
2. 系统提取事实、观点和缺失信息并进行分析。
3. 用户查看三级结论、理由、风险和适用条件。

## Core Features
1. 商品与个人需求输入。
2. 关键优缺点、风险和信息缺口提取。
3. 三级购买结论及适用条件。
4. 事实与推断标记。

## Nice-to-Have
- 比较两个用户手动输入的候选商品。
- 导出分析摘要。

## Non-Goals
- 实时价格、网页抓取、自动电商导入和购买交易。
- 非消费电子品类、专业安全鉴定和财务建议。
- 账号、长期画像、RAG、多 Agent 和向量数据库。

## AI Role
**Classification:** Useful

**Reason:** AI 能把非结构化评价与个人需求整理成一致的判断维度；结论仍必须受固定规则和用户提供的证据约束。

**Fallback:** 使用参数权重表和人工勾选的优缺点生成规则化评分。

## Important Assumptions
- V1 只分析用户主动粘贴的材料，不验证材料真伪。
- “值得”是相对用户需求与输入价格的适配判断，不是客观质量认证。

## Recommended Tech Stack
- **Client:** 单页 React/Next.js 表单与分析结果视图。
- **Server:** 单个分析端点，用于保护密钥和执行 Schema 校验。
- **Data:** 当前会话状态；无需数据库。
- **AI:** 一次结构化分析调用，字段包含 verdict、facts、inferences、pros、cons、unknowns 和 conditions。
- **External services:** None.

## Scope Risk
**Rating:** MEDIUM

**Reasons:**
- 非结构化评价可能长且相互矛盾。
- 购买建议容易被误读为确定事实。
- 不同商品品类的判断维度差异较大。

**Recommended reduction:** V1 限定消费电子商品，只接受用户粘贴资料，不做抓取、实时比价或双商品比较。

## Complexity
- **产品复杂度:** 3 / 5 — 需要清楚呈现判断边界。
- **工程复杂度:** 2 / 5 — 单端点且无持久化和外部服务。
- **AI 复杂度:** 3 / 5 — 结构化分析需区分事实、观点与推断。

## MVP Success Criteria
- 用户提交一件商品后能获得且只获得一个三级结论。
- 每条事实能追溯到用户输入，推断被明确标记。
- 结果至少列出两个相关理由、主要风险和需要补充的信息。

## Known Risks
- **幻觉事实:** 只允许事实字段引用输入内容，其他内容标记为推断。
- **过度确定:** 使用三级结论并展示信息缺口，不输出无条件保证。
```

## DECISIONS.md 示例

```markdown
# Product Decisions

## Decision 1 — V1 限定消费电子
决定：只支持普通消费电子产品。
原因：不同品类需要不同判断标准，宽泛支持会让结论失去一致性。
影响：界面和提示词使用电池、兼容性、性能、保修等通用电子产品维度。

---

## Decision 2 — 资料由用户提供
决定：V1 不抓取商品页面或实时价格。
原因：核心假设是分析是否有帮助，而不是数据采集能力。
影响：必须清楚显示输入资料范围和缺失项。

---

## Decision 3 — 三级结论
决定：结论固定为“值得买”“有条件值得买”“不建议买”。
原因：比连续分数更可行动，又能保留条件性。
影响：响应 Schema、视觉样式和测试用例使用固定枚举。

---

## Decision 4 — 事实与推断分离
决定：响应分别返回 facts 与 inferences，并为事实保留输入片段引用。
原因：减少模型生成内容被误当成商品事实的风险。
影响：无输入依据的内容不得进入 facts。

---

## Decision 5 — 无持久化
决定：分析只存在当前会话。
原因：账号和历史记录不是验证核心判断流程的必要条件。
影响：不建设数据库和身份系统。
```

## TASKS.md 示例

```markdown
# Development Tasks

## Phase 1 — Setup
- [ ] Create the single-page app and analysis endpoint; done when both run locally.
- [ ] Define input and verdict schemas with fixed enums; done when valid and invalid fixtures are correctly accepted or rejected.

## Phase 2 — Core UI
- [ ] Build the product-and-needs form; done when all required inputs and review text can be submitted.
- [ ] Build the verdict view; done when verdict, reasons, risks, unknowns, facts, and inferences render from a fixture.

## Phase 3 — Core Logic
- [ ] Implement structured analysis for consumer electronics; done when the endpoint returns a schema-valid verdict.
- [ ] Add input-grounding instructions and fact citations; done when every returned fact points to supplied text.
- [ ] Connect form submission to results; done when one product completes the end-to-end flow.

## Phase 4 — Product States
- [ ] Validate missing or oversized input; done when the UI gives a specific corrective message.
- [ ] Handle model and schema failures; done when the user can retry without losing inputs.

## Phase 5 — Polish
- [ ] Distinguish facts, inferences, and unknowns visually and accessibly; done when labels do not rely on color alone.

## Phase 6 — Demo
- [ ] Add two contrasting product fixtures; done when one produces a conditional verdict and one exposes insufficient evidence.
- [ ] Run grounding and end-to-end checks; done when all PRODUCT success criteria pass.
```

## BUILD_PROMPT.md 示例

The generated prompt tells a new session to read the three planning files, start at the first unchecked setup task, support only user-supplied consumer-electronics data, use one structured analysis call with fixed verdict enums and fact citations, avoid scraping/accounts/databases/RAG, validate grounding failures, and update only completed tasks.

