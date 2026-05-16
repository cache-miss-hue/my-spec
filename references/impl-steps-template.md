# Implementation Steps Template

Use this structure for `.codex/specs/<project-slug>-impl-steps/`. Generate all three files together so they stay consistent.

## `spec.md`

````markdown
# <项目名> 实施细则 Spec

## Why

说明为什么需要这份实施细则，以及它如何把一级计划变成可执行、可验收的工作。

## What Changes

- 概括当前实施阶段会改变或新增的能力。
- 明确当前阶段与长期愿景的边界。

## Impact

- Affected specs: <受影响的产品能力、流程、领域对象>
- Affected code: <受影响的主要代码层、模块、服务或配置>

## ADDED Requirements

### Requirement: <能力名称>

The system SHALL <清晰、可验证的系统行为>.

#### Scenario: <场景名称>

- **WHEN** <触发条件>
- **THEN** <系统结果>
- **AND** <必要补充结果>

## MODIFIED Requirements

### Requirement: <被修改的既有要求>

说明修改后的要求、原因和兼容边界。

## REMOVED Requirements

### Requirement: <移除的要求>

**Reason**: <为什么移除>
**Migration**: <如果需要，说明替代或迁移路径>
````

## `tasks.md`

````markdown
# Tasks

- [ ] Task 1: <任务名：结果导向描述>
  - [ ] SubTask 1.1: <可执行子任务>
  - [ ] SubTask 1.2: <可执行子任务>

- [ ] Task 2: <任务名：结果导向描述>
  - [ ] SubTask 2.1: <可执行子任务>
  - [ ] SubTask 2.2: <可执行子任务>

# Task Dependencies

- Task 2 depends on Task 1.

# Parallelization Notes

- <哪些任务可并行，前置条件是什么>
````

For existing projects, mark `[x]` only when repository inspection or explicit user confirmation proves the task is already complete.

## `checklist.md`

````markdown
- [ ] <验收项：用户可观察或测试的结果>
- [ ] <验收项：覆盖关键边界条件>
- [ ] <验收项：覆盖失败状态或错误提示>
- [ ] <验收项：覆盖文档、配置或迁移要求>
````

For existing projects, include short progress notes under checked items when useful:

````markdown
- [x] <已完成验收项>
  - 进度：<证据，例如已存在的模块、测试、手动确认或命令结果>
````
