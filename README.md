# Skills

*Each skill is ranked from most to least powerful inside its category.*

## Quality of Life

| Skill | Summary | Install | Codex Specific |
| --- | --- | --- | --- |
| <img src="./plan-my-grill/assets/icon.png" width="40" alt="Plan My Grill icon"><br>**Plan My Grill** | !! WARNING: This is a good skill !! Interrogate plans and designs until they are handoff-ready. | `npx skills@latest add CratesSo/skills/plan-my-grill` | yes |
| <img src="./goal/assets/icon.png" width="40" alt="Goal icon"><br>**Goal** | Design durable Codex self-goals with explicit success and stop conditions. | `npx skills@latest add CratesSo/skills/goal` | yes |
| <img src="./handoff/assets/icon.png" width="40" alt="Handoff icon"><br>**Handoff** | Generate concise continuation prompts from current thread context and tool results. | `npx skills@latest add CratesSo/skills/handoff` | yes |
| <img src="./actions/assets/icon.png" width="40" alt="Actions icon"><br>**Actions** | Manage workspace actions in `.codex/environments/environment.toml`. | `npx skills@latest add CratesSo/skills/actions` | yes |
| <img src="./agents-doctor/assets/icon.png" width="40" alt="Agents Doctor icon"><br>**Agents Doctor** | Audit repo AGENTS.md files for safe cleanup opportunities. | `npx skills@latest add CratesSo/skills/agents-doctor` | no |
| <img src="./html-report/assets/icon.png" width="40" alt="HTML Report icon"><br>**HTML Report** | Generate complete standalone HTML reports from recap or custom requests. | `npx skills@latest add CratesSo/skills/html-report` | no |
| <img src="./todo/assets/icon.png" width="40" alt="Todo icon"><br>**Todo** | Manage a repo-root `todo.md` with durable four-character item references. | `npx skills@latest add CratesSo/skills/todo` | no |

## Code Review

| Skill | Summary | Install | Codex Specific |
| --- | --- | --- | --- |
| <img src="./slop-team-six/assets/icon.png" width="40" alt="Slop Team Six icon"><br>**Slop Team Six** | Run evidence-backed cleanup sweeps using subagents and lane playbooks. | `npx skills@latest add CratesSo/skills/slop-team-six` | no |
| <img src="./audit-team/assets/icon.png" width="40" alt="Audit Team icon"><br>**Audit Team** | Coordinate agentic audit workflows from scope mapping through triage and fixes. | `npx skills@latest add CratesSo/skills/audit-team` | no |
| <img src="./code/assets/icon.png" width="40" alt="Code icon"><br>**Code** | Apply strict engineering constraints for complex coding, risky edits, refactoring, and cleanup. | `npx skills@latest add CratesSo/skills/code` | no |
| <img src="./fix/assets/icon.png" width="40" alt="Fix icon"><br>**Fix** | Investigate technical failures before applying narrow, verified fixes. | `npx skills@latest add CratesSo/skills/fix` | no |
| <img src="./preflight/assets/icon.png" width="40" alt="Preflight icon"><br>**Preflight** | Run production-readiness preflight checks across security, database, deployment, code, and Bandit scanning for Python. | `npx skills@latest add CratesSo/skills/preflight` | no |

## Versions

| Skill | Directory | Current version | Tag |
| --- | --- | --- | --- |
| **actions** | `actions/` | v1.0.7 | `actions/v1.0.7` |
| **agents-doctor** | `agents-doctor/` | v1.0.6 | `agents-doctor/v1.0.6` |
| **audit-team** | `audit-team/` | v1.5.3 | `audit-team/v1.5.3` |
| **code** | `code/` | v1.0.0 | `code/v1.0.0` |
| **fix** | `fix/` | v1.0.1 | `fix/v1.0.1` |
| **goal** | `goal/` | v1.0.1 | `goal/v1.0.1` |
| **handoff** | `handoff/` | v2.0.0 | `handoff/v2.0.0` |
| **plan-my-grill** | `plan-my-grill/` | v1.6.3 | `plan-my-grill/v1.6.3` |
| **preflight** | `preflight/` | v1.0.4 | `preflight/v1.0.4` |
| **html-report** | `html-report/` | v1.1.1 | `html-report/v1.1.1` |
| **slop-team-six** | `slop-team-six/` | v2.0.5 | `slop-team-six/v2.0.5` |
| **todo** | `todo/` | v0.1.2 | `todo/v0.1.2` |

## Install / Pin

Install a skill from this repo with `npx skills@latest add`.

Examples:

- `npx skills@latest add CratesSo/skills/actions`
- `npx skills@latest add CratesSo/skills/plan-my-grill`

Use the matching tag when pinning a published version.

Examples:

- `CratesSo/skills@actions/v1.0.7`
- `CratesSo/skills@plan-my-grill/v1.6.3`
