# BUILD_PROMPT.md Template

Create a prompt that can be pasted into a new AI coding session without relying on the planning conversation. It should direct the session to the four local documents, preserve scope, and define the next executable action.

```markdown
# Build Task

你正在实现当前目录中 `PRODUCT.md` 定义的 MVP。

## 开始前

按顺序完整阅读：

1. `PRODUCT.md` — 产品范围、核心流程、成功标准与 Non-Goals
2. `DECISIONS.md` — 已确定且会约束实现的产品与技术决策
3. `TASKS.md` — 按依赖排序的开发任务与完成条件

先检查现有项目状态，不要重新创建已经存在的结构或覆盖用户修改。

如果三份文件存在冲突，先停止实现，指出具体冲突，并以 `PRODUCT.md` 的产品范围为基准提出最小修正。不要静默扩大范围。

## 实现规则

- 遵守 `PRODUCT.md` 定义的目标用户、核心流程、Core Features 和技术边界。
- 遵守 `DECISIONS.md` 中已经确定的决策；需要改变时先说明原因及影响。
- 不实现 `Nice-to-Have` 或 `Non-Goals` 中的内容。
- 按 `TASKS.md` 的依赖顺序开发，从编号最靠前且依赖已满足的未完成 `T-*` 任务开始。
- 每个阶段结束时保持项目可运行。
- 优先选择满足需求的最简单实现，不为展示技术增加架构复杂度。
- 未经明确要求，不新增账号、支付、后台、RAG、多 Agent、MCP、微服务或其他基础设施。

## 当前目标

完成 `TASKS.md` 中第一个未完成阶段，并明确列出本轮涉及的 `T-*`、`CF-*` 和 `SC-*` ID。不要提前实现后续阶段。

## 完成阶段后的检查

1. 运行项目或最接近的可执行检查。
2. 检查并修复由本阶段引入的阻塞错误。
3. 对照任务的完成条件验证结果。
4. 在 `TASKS.md` 中只勾选已验证完成的任务。
5. 汇总修改、验证结果、剩余风险和下一阶段。

## 产品特定约束

- AI Role: <copy classification and boundary from PRODUCT.md>
- Persistence: <copy the decided storage boundary>
- External services: <list only required services, or “None”>
- Critical failure behavior: <copy the relevant decision>
```

Replace all angle-bracket placeholders with facts from `PRODUCT.md` and `DECISIONS.md`. Do not duplicate the entire documents; include only the constraints needed to prevent drift if the files are present. The prompt is self-contained when a new session knows what to read, what not to change, where to start, and how to verify completion.
