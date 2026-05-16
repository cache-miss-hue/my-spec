# My Spec

中文 | [English](#english)

`my-spec` 是一个 Codex Skill，也可以作为通用 Agent 工作流提示词使用。它用于把松散的项目想法整理成可确认的一级计划，并在用户确认后继续生成可执行、可验收的实施细则。

它默认用中文工作，适合在项目早期把目标、范围、目录结构、实施任务和验收标准先说清楚，避免直接进入零散编码。

## 功能

- 生成 `.codex/<project-slug>-1st-plan.md` 一级项目计划。
- 在确认一级计划后，生成 `.codex/specs/<project-slug>-impl-steps/` 下的实施文件：
  - `spec.md`
  - `tasks.md`
  - `checklist.md`
- 在写文件前先探索当前项目结构，并尽量只问无法从仓库判断的问题。
- 强制区分当前范围、延期范围、关键决策、领域模型、目录结构和验证计划。
- 可作为通用 Agent 提示词流程迁移到 Claude、Cursor、ChatGPT、Gemini 或其他 AI 编程助手中。

## 适用场景

- 你想开始一个新项目，但还没有清晰的实施边界。
- 你想把已有项目的改造需求整理成计划和任务。
- 你希望 Agent 在动手写代码前先形成可审查、可回滚、可验收的规格说明。

## 安装

把本仓库克隆或复制到你的 Codex skills 目录中，例如：

```powershell
git clone https://github.com/cache-miss-hue/my-spec.git C:\Users\<you>\.codex\skills\my-spec
```

如果你使用的是其他 `CODEX_HOME`，请把目标路径替换为：

```text
%CODEX_HOME%\skills\my-spec
```

安装后，重新启动 Codex 会话或刷新 skills 索引。

## 使用

在项目目录中对 Codex 说：

```text
使用 $my-spec，帮我为这个项目生成一级计划。
```

或者直接描述需求：

```text
我想做一个项目计划：……
```

默认流程分为两段：

1. 先生成一级计划。这个阶段只明确目标、范围、关键决策、目录结构和验证方案。
2. 用户确认一级计划后，再生成实施细则、任务清单和验收 checklist。

## 通用 Agent 用法

如果你的工具不支持 Codex Skill，可以把 `SKILL.md` 和 `references/` 中的模板作为通用工作流提示词使用。

推荐做法：

1. 把 `SKILL.md` 的正文放进 Agent 的项目规则、系统提示词或自定义指令中。
2. 告诉 Agent 在生成一级计划时参考 `references/first-plan-template.md`。
3. 告诉 Agent 在生成实施细则时参考 `references/impl-steps-template.md`。
4. 保留“两阶段”规则：先确认一级计划，再生成实施细则。

## 目录结构

```text
my-spec/
  SKILL.md                         # Skill 入口和工作流规则
  agents/
    openai.yaml                    # OpenAI/Codex 侧展示信息
  references/
    first-plan-template.md         # 一级计划模板
    impl-steps-template.md         # 实施细则模板
```

## 设计原则

- 先澄清目标和边界，再生成文件。
- 优先读仓库已有上下文，少问可从文件判断的问题。
- 不覆盖已有 `.codex` 产物，避免误伤用户已有计划。
- 不安装依赖、不改密钥、不执行破坏性命令。
- 计划和任务必须能被后续实现者直接执行和验收。

## 贡献

欢迎提交 issue 或 pull request。修改工作流规则时，请优先保持行为小而明确，避免把 skill 变成泛化的项目管理模板。

详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 致谢

感谢 [Matt Pocock](https://github.com/mattpocock) 的 [`grill-me`](https://github.com/mattpocock/skills) skill。`my-spec` 的提问式澄清流程受到它的启发：在生成计划前，先通过逐步追问把目标、约束和取舍确认清楚。

## 许可证

本项目使用 [MIT License](LICENSE)。

---

## English

[中文](#my-spec) | English

`my-spec` is a Codex Skill that can also be used as a general agent workflow prompt. It turns a loose project idea into a confirmed first plan, then optionally into implementation-ready spec files after user confirmation.

It defaults to Chinese, but the workflow can be used in any language required by the target project.

## Features

- Generates a first project plan at `.codex/<project-slug>-1st-plan.md`.
- After the first plan is confirmed, generates implementation files under `.codex/specs/<project-slug>-impl-steps/`:
  - `spec.md`
  - `tasks.md`
  - `checklist.md`
- Explores the existing project before writing files or asking questions.
- Separates current scope, deferred scope, key decisions, domain model, directory structure, and validation plan.
- Can be adapted for Claude, Cursor, ChatGPT, Gemini, or other AI coding agents.

## Use Cases

- You want to start a new project but the implementation boundary is still unclear.
- You want to turn a refactor or migration idea into a plan and task list.
- You want an agent to produce reviewable, reversible, and verifiable specs before writing code.

## Installation

Clone or copy this repository into your Codex skills directory:

```powershell
git clone https://github.com/cache-miss-hue/my-spec.git C:\Users\<you>\.codex\skills\my-spec
```

If you use a custom `CODEX_HOME`, replace the target path with:

```text
%CODEX_HOME%\skills\my-spec
```

Restart your Codex session or refresh the skills index after installation.

## Usage

In a project directory, ask Codex:

```text
Use $my-spec to generate a first plan for this project.
```

Or describe your project idea directly:

```text
I want to create a project plan for...
```

The workflow has two stages:

1. Create only the first plan. This stage clarifies goals, scope, key decisions, directory structure, and validation.
2. After the user confirms the first plan, generate the implementation spec, task list, and acceptance checklist.

## General Agent Usage

If your tool does not support Codex Skills, use `SKILL.md` and the templates under `references/` as a general workflow prompt.

Recommended setup:

1. Put the body of `SKILL.md` into your agent's project rules, system prompt, or custom instructions.
2. Tell the agent to use `references/first-plan-template.md` when drafting the first plan.
3. Tell the agent to use `references/impl-steps-template.md` when drafting implementation details.
4. Keep the two-stage rule: confirm the first plan before generating implementation details.

## Directory Structure

```text
my-spec/
  SKILL.md                         # Skill entrypoint and workflow rules
  agents/
    openai.yaml                    # OpenAI/Codex display metadata
  references/
    first-plan-template.md         # First plan template
    impl-steps-template.md         # Implementation steps template
```

## Design Principles

- Clarify goals and boundaries before writing files.
- Prefer repository discovery over asking questions that can be answered from existing files.
- Do not overwrite existing `.codex` artifacts.
- Do not install dependencies, edit secrets, or run destructive commands.
- Plans and tasks should be executable and verifiable by the next implementer.

## Contributing

Issues and pull requests are welcome. Keep workflow changes small and explicit, and avoid turning this skill into a generic project management template.

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Acknowledgements

Thanks to [Matt Pocock](https://github.com/mattpocock) for the [`grill-me`](https://github.com/mattpocock/skills) skill. The question-driven clarification flow in `my-spec` was inspired by it: before generating a plan, clarify goals, constraints, and tradeoffs through step-by-step questioning.

## License

This project is licensed under the [MIT License](LICENSE).
