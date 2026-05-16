# First Plan Template

Use this structure for `.codex/<project-slug>-1st-plan.md`. Keep sections concise but decision-complete. Rename headings only when the project context makes a different heading clearer.

````markdown
# <项目名>：<一句话计划标题>

## 项目总目标

说明项目要解决什么问题、为谁服务、最终希望达到什么状态。不要只写功能列表，要写清楚为什么这个项目值得做。

## 当前实施重点

说明当前阶段优先交付的最小可用闭环。列出核心用户路径或核心工作流。

## Key Decisions

- 记录已经确定的重要产品、技术、范围和风险决策。
- 每条决策要能影响后续实现，而不是泛泛描述。

## Domain Model

- `核心概念`：用项目领域语言解释重要实体、状态、关系和边界。
- 如果项目很小，可以只列最关键的概念。

## Directory Tree

```text
<project-root>/
  <dir-or-file>/        # 简要说明职责
  <dir-or-file>/        # 简要说明职责
```

说明规则：

- 空项目或新项目：写目标目录结构。
- 已有项目、迁移、重构：先反映当前实际结构，再写必要的目标调整。
- 只写关键目录和关键文件，不要把依赖目录、构建产物、缓存目录塞进计划。

## Implementation Changes

- 写当前阶段需要新增、修改或串联的主要能力。
- 按行为或子系统分组，不要写成过细的逐文件清单。

## Deferred

- 写明确不在当前阶段做的内容。
- 延后项要避免误伤当前验收边界。

## Docs To Update During Implementation

- 写需要同步创建或更新的项目文档、上下文文件、ADR、README、用户说明等。

## Test Plan

- 写可验证的场景。
- 覆盖主流程、关键边界条件、失败状态和最小回归验证。
````
