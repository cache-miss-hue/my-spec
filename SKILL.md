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
- Ask one important question at a time, and include the recommended answer.
- Keep challenging unclear intent, scope, boundaries, constraints, success criteria, risks, and tradeoffs until the next artifact is decision-complete.
- Do not write files until the user confirms the artifact summary or final draft.
- Do not overwrite existing `.codex` artifacts. If a target file or directory exists, read it first and ask whether to update it, create a versioned copy, or stop.
- Do not install dependencies, change secrets, run destructive commands, or modify unrelated project files as part of this workflow.

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
3. Interview the user until the first plan is clear:
   - Goal and target users.
   - Core workflows and success criteria.
   - Current state and constraints.
   - In scope, out of scope, and deferred work.
   - Major design, data, architecture, or product tradeoffs.
4. Draft the first plan using `references/first-plan-template.md`.
5. Include a `Directory Tree` section:
   - For empty or new projects, describe the target project structure.
   - For existing, migration, or refactor projects, first reflect the actual structure and then describe necessary target changes.
   - Add short explanations for important directories.
6. Present a concise summary or full draft for confirmation.
7. After confirmation, write `.codex/<project-slug>-1st-plan.md`.

## Stage 2: Implementation Steps

Trigger Stage 2 only when the user has confirmed the first plan and explicitly asks to continue, generate implementation details, create spec files, split tasks, generate checklist, or similar.

1. Read the confirmed first plan and current project state.
2. Re-interview the user with the same strict questioning rules, now focused on implementation decisions:
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
