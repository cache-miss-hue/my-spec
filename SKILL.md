---
name: my-spec
description: Create rigorous project plans and implementation specs for Codex projects. Use when the user asks to create a project plan, start a project, define a project spec, write an implementation plan, generate tasks/checklists, or says things like "创建一个项目计划", "我想做一个项目", "生成 spec", "生成实施细则", "拆 tasks", or explicitly invokes $my-spec. For casual project brainstorming, first confirm whether to enter the my-spec workflow.
---

# My Spec

Use this skill to turn a loose project idea into a confirmed first plan, then optionally into implementation-ready spec files. Default to Chinese unless the user asks otherwise or the target project requires another language.

## Operating Rules

- Work in two stages. Stage 1 creates only the first plan. Stage 2 creates implementation details only after the user confirms the first plan and explicitly asks to continue.
- Explore before asking. Read current project files, manifests, README files, existing `.codex` artifacts, and likely entrypoints before asking questions.
- Ask only questions that cannot be answered from the repository or system context.
- Run an interview loop before drafting. Ask one important question at a time, include your recommended answer, then use the user's response to decide the next highest-impact unknown.
- Continue the interview until the next artifact is decision-complete. Do not stop after a fixed number of questions.
- Keep challenging unclear intent, scope, boundaries, constraints, success criteria, risks, and tradeoffs. If any of these are vague, contradictory, or missing, ask another question instead of drafting.
- Do not draft or write the next artifact until you can fill every required section with concrete, non-placeholder content.
- Do not write files until the user confirms the artifact summary or final draft.
- Do not overwrite existing `.codex` artifacts. If a target file or directory exists, read it first and ask whether to update it, create a versioned copy, or stop.
- Do not install dependencies, change secrets, run destructive commands, or modify unrelated project files as part of this workflow.

## Interview Loop

Use this loop in both stages:

1. Build the current understanding from the repository, prior conversation, and any existing plan/spec files.
2. Identify the single most important unresolved decision that blocks a decision-complete artifact. Walk down each branch of the design tree, resolving dependencies between decisions one by one before asking downstream questions.
3. Ask exactly one question about that decision.
4. Include the recommended answer and briefly explain the tradeoff.
5. After the user answers, update the current understanding and repeat the loop.
6. Exit the loop only when all readiness checks for the current stage pass.

Ask follow-up questions when the answer introduces new ambiguity, conflicts with repository evidence, expands scope, changes constraints, or leaves acceptance criteria unclear.

Do not combine multiple unrelated decisions into one question. If several decisions are blocked, ask them one at a time in dependency order.

If a question can be answered by exploring the codebase, explore the codebase instead of asking the user.

### Required Question Format

Interview the user relentlessly about every aspect of the plan until there is a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one by one. For each question, provide your recommended answer.

When several realistic options exist, present the options clearly and still provide your recommendation. Let the user accept the recommendation, choose another option, ask a follow-up question, or provide a different answer.

Prefer this format:

```markdown
问题：<one important unresolved decision>

可选方向：
- A. <option A>
- B. <option B>
- C. <option C>
- D. 其他：直接描述你的想法

推荐：<the option or answer you recommend, with assumptions if needed>

理由：<why this recommendation is likely best, including the key tradeoff>

如果你同意，我会按这个继续追问下一个关键问题；如果不同意，你可以选其他方向，或选 D 直接补充你的答案。
```

When the decision is not naturally multiple-choice, ask a focused open question and still include a recommended answer:

```markdown
问题：这个项目当前阶段的最小可用闭环应该到哪里为止？

推荐：先做到 <recommended boundary>，把 <deferred work> 放进 Deferred。

理由：这样能先验证 <core value>，同时避免当前阶段被 <main risk> 拖大。
```

## Stage 1 Readiness Check

Before drafting the first plan, confirm that these items are concrete enough to write without placeholders:

- Project goal, target users, and the problem being solved.
- Minimum useful workflow for the current stage.
- In-scope, out-of-scope, and deferred work.
- Success criteria and user-visible acceptance signals.
- Key product and technical decisions that affect implementation.
- Main domain concepts, states, relationships, and boundaries.
- Current or target directory structure.
- Documentation and validation expectations.

If any item is missing, ask another interview question.

## Stage 2 Readiness Check

Before drafting implementation steps, confirm that these items are concrete enough to write without placeholders:

- Interfaces, commands, screens, APIs, schemas, or file formats that will change.
- Data flow and state transitions.
- Error cases, edge cases, and failure behavior.
- Migration or compatibility requirements, if any.
- Acceptance criteria for each major behavior.
- Which existing work is already complete and how that was verified.
- Task dependencies and safe parallelization boundaries.

If any item is missing, ask another interview question.

## Stage 1: First Plan

Trigger Stage 1 when the user asks to create a project plan, start a project, define a new project, or explicitly invokes `$my-spec`.

1. Discover context:
   - Identify whether the current directory is empty, a new scaffold, or an existing project.
   - Look for project names in manifests such as `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, README files, or the current directory name.
   - Inspect existing `.codex` plans and specs if present.
2. Determine the project slug:
   - Prefer a user-provided project name.
   - Otherwise use a manifest name.
   - Otherwise use the current directory name.
   - If multiple plausible names conflict, ask the user to choose.
3. Interview the user until the Stage 1 readiness check passes:
   - Goal and target users.
   - Core workflows and success criteria.
   - Current state and constraints.
   - In scope, out of scope, and deferred work.
   - Major design, data, architecture, or product tradeoffs.
4. Draft the first plan using `references/first-plan-template.md` only after the Stage 1 readiness check passes.
5. Include a `Directory Tree` section:
   - For empty or new projects, describe the target project structure.
   - For existing, migration, or refactor projects, first reflect the actual structure and then describe necessary target changes.
   - Add short explanations for important directories.
6. Present a concise summary or full draft for confirmation.
7. After confirmation, write `.codex/<project-slug>-1st-plan.md`.

## Stage 2: Implementation Steps

Trigger Stage 2 only when the user has confirmed the first plan and explicitly asks to continue, generate implementation details, create spec files, split tasks, generate checklist, or similar.

1. Read the confirmed first plan and current project state.
2. Re-interview the user until the Stage 2 readiness check passes, now focused on implementation decisions:
   - Interfaces, schemas, data flow, file layout, migrations, edge cases, failures, validation, and acceptance criteria.
3. For existing projects, inspect current code and mark already-complete work accurately.
4. Generate the implementation directory:
   - `.codex/specs/<project-slug>-impl-steps/spec.md`
   - `.codex/specs/<project-slug>-impl-steps/tasks.md`
   - `.codex/specs/<project-slug>-impl-steps/checklist.md`
5. Use `references/impl-steps-template.md`.
6. In `tasks.md` and `checklist.md`, use `[x]` only when repository inspection or user confirmation supports that the work is already done.

## Artifact Naming

- First plan: `.codex/<project-slug>-1st-plan.md`
- Implementation spec directory: `.codex/specs/<project-slug>-impl-steps/`
- Use lowercase slug names with words separated by hyphens.
- If the user asks for a different name, use their requested name after normalizing unsafe filename characters.

## References

- Read `references/first-plan-template.md` when drafting the Stage 1 plan.
- Read `references/impl-steps-template.md` when drafting Stage 2 implementation files.
