# Spec Kit Setup Guide

Set up [Spec Kit](https://github.com/github/spec-kit) for spec-driven development in this React Native project.

---

## Prerequisites

- **Python 3.11+** — [python.org/downloads](https://www.python.org/downloads/)
- **uv** — [docs.astral.sh/uv](https://docs.astral.sh/uv/) (Python package/tool manager)
- **Git** — [git-scm.com](https://git-scm.com/downloads)

## 1. Install the Specify CLI

### Option A — Persistent install (recommended)

Pin a [stable release tag](https://github.com/github/spec-kit/releases):

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z
```

To upgrade later:

```bash
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git@vX.Y.Z
```

### Option B — One-time run

```bash
uvx --from git+https://github.com/github/spec-kit.git@vX.Y.Z specify init <PROJECT_NAME>
```

### Verify

```bash
specify check
```

## 2. Initialize in This Project

Run from the repo root:

```bash
# Initialize with GitHub Copilot support (bash/zsh)
specify init --here --ai copilot

# On Windows, add PowerShell scripts
specify init --here --ai copilot --script ps
```

This creates the `.specify/` directory structure and installs Spec Kit slash commands for Copilot.

### Optional: Install as agent skills

```bash
specify init --here --ai copilot --ai-skills
```

## 3. Workflow Overview

After initialization, these slash commands are available in Copilot Chat:

| Step | Command | Purpose |
|------|---------|---------|
| 1 | `/speckit.constitution` | Define project principles and guidelines (once per repo) |
| 2 | `/speckit.specify` | Describe the feature — what and why, not how |
| 3 | `/speckit.clarify` | *(Optional)* Surface underspecified areas |
| 4 | `/speckit.plan` | Add tech stack choices and create implementation plan |
| 5 | `/speckit.analyze` | *(Optional)* Cross-check spec ↔ plan consistency |
| 6 | `/speckit.tasks` | Generate atomic, testable implementation tasks |
| 7 | `/speckit.implement` | Execute all tasks and build the feature |

### Additional commands

| Command | Purpose |
|---------|---------|
| `/speckit.checklist` | Generate quality checklists ("unit tests for English") |

## 4. Example — New Feature

```text
# Step 1: Define what you want (paste in Copilot Chat)
/speckit.specify Build a photo album app where albums are grouped by date
and can be reordered via drag-and-drop on the main page. Albums are never
nested. Each album shows photos in a tile grid.

# Step 2: Add tech stack
/speckit.plan Use React Native with TypeScript, React Navigation,
react-native-reanimated for drag gestures, and Zustand for state.
Images stored locally, metadata in SQLite via expo-sqlite.

# Step 3: Generate tasks
/speckit.tasks

# Step 4: Build it
/speckit.implement
```

## 5. React Native–Specific Constitution Tips

When running `/speckit.constitution`, include principles like:

- All components must be functional with TypeScript strict mode
- Use `StyleSheet.create` — no inline styles
- Theme tokens from `src/theme/` for colors, spacing, typography
- Accessibility labels and roles on all interactive elements
- Co-located tests with React Native Testing Library
- React Navigation v6+ with typed `RootStackParamList`

## 6. Project Structure After Init

```
.specify/
├── templates/         # Spec Kit templates (auto-generated)
└── overrides/         # Project-local template overrides

# Feature artifacts (created per feature branch):
constitution.md        # Project principles
spec.md               # Feature specification
plan.md               # Technical implementation plan
tasks.md              # Task breakdown
```

## 7. Extensions & Presets

Customize Spec Kit's behavior:

```bash
# Browse available extensions
specify extension search

# Install an extension (e.g., Jira integration)
specify extension add <extension-name>

# Browse available presets
specify preset search

# Install a preset (e.g., compliance-oriented specs)
specify preset add <preset-name>
```

## 8. Copilot Agents

This repo includes a dedicated **`@speckit-designer`** agent that understands the Spec Kit workflow and React Native context. Use it for complex multi-step spec-driven work:

```text
@speckit-designer Help me specify and plan the push notification feature
```

The **`/spec-to-code`** skill provides a quick-start guide for the full workflow.

## 9. Troubleshooting

| Issue | Fix |
|-------|-----|
| `specify: command not found` | Run `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z` |
| `uv: command not found` | Install uv: `curl -LsSf https://astral.sh/uv/install.sh \| sh` (or `powershell -c "irm https://astral.sh/uv/install.ps1 \| iex"` on Windows) |
| Slash commands not showing | Run `specify init --here --ai copilot --force` to re-install, then reload VS Code |
| `SPECIFY_FEATURE` error | Set the env var to your feature dir name if not using Git branches |
| Agent doesn't use Spec Kit | Ensure `github.copilot.chat.agent.useProjectAgents` is `true` in `.vscode/settings.json` |

## Resources

- [Spec Kit README](https://github.com/github/spec-kit)
- [Spec-Driven Development methodology](https://github.com/github/spec-kit/blob/main/spec-driven.md)
- [Extensions catalog](https://github.com/github/spec-kit/blob/main/extensions/README.md)
- [Presets catalog](https://github.com/github/spec-kit/blob/main/presets/README.md)
- [Video overview](https://www.youtube.com/watch?v=a9eR1xsfvHg)
