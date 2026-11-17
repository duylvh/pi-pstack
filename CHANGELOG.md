# @duylvh/pi-pstack

## 0.11.0

### Minor Changes

- Sync Cursor pstack 0.15.43 (`e1cc031`). Skill texts are shorter, `how` and `why` each fit in one file, `poteto-mode/worker.md` carries the operator's rules into every agent kickoff, and the Orchestrate playbook and `check-plan.mjs` are gone.
- Retire the roles upstream no longer reads: `how explorer`, `how explainer`, `why investigators`, `why synthesizer`, `reflect tooling`, `reflect judgment, divergent, synthesizer`, and `architect runners`. The extension ignores them without a warning, so an existing `models.json` still loads. `how` now reads `judgment and prose`.
- Port the new upstream text to Pi: arena runners and judge, the `how` explainer spawn, the kickoff rule for `Agent` and `SubagentWorkflow` agents, and `deslop` and verification routing. The Cursor default-model list is dropped from `poteto-mode`, and `gemini-*` slugs now count as Cursor leftovers.
- Drop the `tools-package-test` rule, now that upstream ships the same test script.

## 0.10.0

### Minor Changes

- Rename the package to `@duylvh/pi-pstack`, with its script packages `@duylvh/pi-pstack-tools` and `@duylvh/pi-pstack-statechart`. Pi keys the install by its Git source, so existing installs keep working. The reground script writes the new names, so a Cursor sync keeps them.

## 0.9.1

### Patch Changes

- Align the subagent rules with `@tintinweb/pi-subagents` 0.26.
  - Worktree safety: never resume a worktree agent for a follow-up. Its worktree is deleted when it finishes, so `Agent` refuses the resume or runs it unisolated in the coordinator's checkout. Orchestrate no longer resumes a worker for its worktree.
  - `pi-runtime.md`: a finished delegate's result survives a restart through `get_subagent_result`. A new Workflows section maps pstack's spawn rules onto `SubagentWorkflow` `agent()` options for when the user asks for a workflow.
  - poteto-mode defaults: fan out through `Agent`, not `SubagentWorkflow`, unless the user asked for a workflow.

## 0.9.0-duylvh.1

### Minor Changes

- Port the extension improvements from zenspc/pi-extensions 0.9.0, kept compatible with `@tintinweb/pi-subagents`.
  - Restore Poteto Mode on `/tree` navigation and before every turn, state it explicitly when off, and keep the skill path in the prompt after compaction.
  - Turn the mode off only on an exact `off`, `disable`, or `stop`, so tasks that start with those words still run.
  - Refuse to activate the mode when the pstack skills are not loaded.
  - Hide skills and inject the role table through Pi 1.4's structured system prompt instead of regex-stripping the rendered prompt.
  - Keep inherited panel seats, report config problems once, refuse to overwrite a broken `models.json`, and expand `/pstack status`.
- Add `pi-models.md` and `pi-runtime.md` guides, written for the `Agent` tool, and link them from the skills that need them. The sync script keeps both.
- Skip zenspc's per-model thinking suffixes and `pi-subagents` acceptance rules, which target a different subagent package.

## 0.8.0-duylvh.1

### Minor Changes

- Sync Cursor pstack 0.15.36 and split pi-pstack into its own repository.

## 0.6.0

### Minor Changes

- 79943ee: Sync Cursor pstack 0.15.0. Add Attack the Premise and Test Behavior, Not Implementation. Drop how Critique Mode. Ship a re-ground lever for the next pull.

## 0.5.0

### Minor Changes

- 512f93b: Port Cursor pstack's forge-neutral PR playbooks, the verified multi-phase plan checklist, and TypeScript schema-at-boundary guidance.

## 0.4.0

### Minor Changes

- 818fef3: Hide 41 Pstack skills from the Skill catalog. `/pstack on` restores `how`, `why`, `unslop`, and `typescript-best-practices` only.

### Patch Changes

- 818fef3: Inject Cursor's Poteto Mode one-liner instead of the Skill body mandate. Skip the role table when every role inherits.

## 0.3.0

### Minor Changes

- 0ad52fa: Add `/pstack on|off|status` to hide pstack skill descriptions from the system prompt and persist the choice.

## 0.2.0

### Minor Changes

- eaec816: Add the deslop skill for AI code-slop cleanup.

  Point poteto-mode's before-commit trigger at `/skill:deslop`. Keep `/skill:unslop` on prose.

## 0.1.0

### Minor Changes

- 363ded6: New package: pstack for Pi. Ports the Cursor pstack plugin as 44 Agent Skills standard skills (poteto-mode with 22 playbooks, workflow skills, 21 principle skills) plus two pi-subagents agent definitions (poteto-agent, comment-sicko).
