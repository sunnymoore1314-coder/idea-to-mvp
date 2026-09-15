# Example — Expense Splitter

## Input

> 我想做一个 AI 工具，帮朋友聚餐后平分费用。

## Mode

`Create` — 当前没有既有产品文档。

## Refined Idea

一个面向小型朋友聚餐的费用平分工具，记录参与者、付款金额和个人消费项，使用确定性规则计算每个人应付或应收金额，并生成最少转账建议。

## Clarification Result

### Known Facts

- 用户希望解决朋友聚餐后的费用分摊。
- 原始想法提到 AI，但没有需要理解或生成非结构化内容的核心步骤。

### Important Assumptions

- **A-01 — V1 处理单次聚餐：** Confidence: High. Impact if wrong: 需要增加长期账本和持久化。
- **A-02 — 金额使用同一种货币：** Confidence: Medium. Impact if wrong: 需要汇率来源和时间规则。

### Blocking Questions

None. 两项假设都不会改变 V1 的主要用户或核心流程。

## AI Role

**Classification:** Unnecessary

**Reason:** 费用合计、个人消费分配和净额结算都是确定性计算，使用 AI 会降低可解释性并增加错误风险。

**No-AI baseline:** 使用十进制金额运算和明确的分摊规则计算余额，再用贪心算法生成转账建议。

**AI boundary:** None.

## Scope Risk

**LOW** — 单一用户流程、无账号、无支付、无外部 API，所有计算均可在本地完成。

## Complexity

- **产品复杂度:** 2 / 5 — 主要难点是清晰表达分摊规则。
- **工程复杂度:** 2 / 5 — 本地表单、确定性计算和结果页面。
- **AI 复杂度:** 1 / 5 — 不使用 AI。

## PRODUCT.md 核心摘录

```markdown
# Product

## 产品名称
聚餐平分（暂定）

## 优化后的 MVP 定义
一个为单次朋友聚餐记录参与者、付款和个人消费，并计算净额与最少转账建议的本地工具。

## Target User
需要在一次聚餐后快速完成费用结算的朋友小组组织者。

## Core User Flow
1. 添加参与者。
2. 录入付款人、金额和分摊对象。
3. 检查录入总额。
4. 查看每个人的净额和建议转账。

## Core Features
- **CF-01:** 添加、修改和删除本次聚餐的参与者。
- **CF-02:** 录入费用并选择平均分摊或指定参与者分摊。
- **CF-03:** 使用确定性规则计算每个人的应付、已付和净额。
- **CF-04:** 生成能结清全部余额的转账建议。

## Non-Goals
- 用户账号、长期账本和跨设备同步。
- 直接发起支付或读取银行账户。
- 多币种换算、票据识别和 AI 分析。

## AI Role
**Classification:** Unnecessary

**Reason:** 核心流程只需要可审计的算术和结算规则。

**No-AI baseline:** 整个 MVP 使用本地确定性计算。

**AI boundary:** None.

## MVP Success Criteria
- **SC-01:** 用户能为至少 2–10 人录入一次聚餐费用并得到结算结果。
- **SC-02:** 所有人的净额之和为零，允许的误差不超过最小货币单位。
- **SC-03:** 建议转账执行后，每个人的余额都归零。
```

## DECISIONS.md 核心摘录

```markdown
# Product Decisions

## Decision D-01 — 不使用 AI
状态：Confirmed

决定：所有金额和转账建议使用确定性算法计算。

原因：结果必须可复现、可解释并满足守恒关系。

影响：项目不包含模型调用、提示词、AI SDK 或相关失败状态。

---

## Decision D-02 — 金额不使用浮点数
状态：Assumed

决定：金额转换为最小货币单位的整数后计算。

原因：避免二进制浮点舍入导致余额无法归零。

影响：输入和显示层负责金额格式转换。
```

## TASKS.md 核心摘录

```markdown
# Development Tasks

## Phase 1 — Calculation Contract
- [ ] **T-01** `[CF-02][CF-03]` Define integer-based expense and split schemas; done when fixtures cover equal and selected-person splits.
- [ ] **T-02** `[CF-03]` Implement balance calculation; done when every fixture preserves a zero total balance.
- [ ] **T-03** `[CF-04]` Implement transfer suggestions; done when applying all transfers clears every balance.

## Phase 2 — Core Interface
- [ ] **T-04** `[CF-01]` Build participant editing; done when 2–10 unique participants can be maintained.
- [ ] **T-05** `[CF-02]` Build expense entry; done when users can choose payer and split participants.
- [ ] **T-06** `[CF-03][CF-04]` Render balances and transfers; done when results update after each valid edit.

## Phase 3 — States and Demo
- [ ] **T-07** `[STATE]` Handle invalid amounts and incomplete expenses; done when calculation is blocked with a specific message.
- [ ] **T-08** `[SC-01][SC-02][SC-03]` Run representative fixtures; done when all success criteria pass.

## Coverage Matrix

| Core Feature | Task IDs | Success Criteria |
| --- | --- | --- |
| CF-01 | T-04 | SC-01 |
| CF-02 | T-01, T-05 | SC-01 |
| CF-03 | T-01, T-02, T-06 | SC-02 |
| CF-04 | T-03, T-06 | SC-03 |
```

## Validation Result

- Product direction is different from both generation and evidence-analysis examples.
- AI is classified as `Unnecessary` and no task introduces an AI dependency.
- All four Core Features map to tasks and success criteria.
- Accounts, payments, persistence, OCR, and multi-currency support remain outside V1.
