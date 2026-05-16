# My Spec

`my-spec` 是一个 Codex Skill，用来把松散的项目想法整理成可确认的一级计划，并在用户确认后继续生成可执行、可验收的实施细则。

它默认用中文工作，适合在项目早期把目标、范围、目录结构、实施任务和验收标准先说清楚，避免直接进入零散编码。

## 功能

- 生成 `.codex/<project-slug>-1st-plan.md` 一级项目计划。
- 在确认一级计划后，生成 `.codex/specs/<project-slug>-impl-steps/` 下的实施文件：
  - `spec.md`
  - `tasks.md`
  - `checklist.md`
- 在写文件前先探索当前项目结构，并尽量只问无法从仓库判断的问题。
- 强制区分当前范围、延期范围、关键决策、领域模型、目录结构和验证计划。

## 适用场景

- 你想开始一个新项目，但还没有清晰的实施边界。
- 你想把已有项目的改造需求整理成计划和任务。
- 你希望 Codex 在动手写代码前先形成可审查、可回滚、可验收的规格说明。

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

感谢 [Matt Pocock](https://github.com/mattpocock) 的 [`grill-me`](https://github.com/mattpocock/skills) skill。`my-
spec` 的提问式澄清流程受到它的启发：在生成计划前，先通过逐步追问把目标、约束和取舍确认清楚。
## 许可证

本项目使用 [MIT License](LICENSE)。
