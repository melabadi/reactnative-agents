# GitHub Copilot Setup for React Native Toolkit

This directory configures GitHub Copilot agents, skills, MCP servers, and VS Code settings for React Native development with Spec Kit and Rovo integration.

## Structure

```
.github/
├── copilot-instructions.md              # Repo-wide coding conventions for Copilot
├── agents/
│   ├── rn-architect.agent.md            # Architecture design & review
│   ├── rn-debugger.agent.md             # Crash & error diagnosis
│   ├── rn-reviewer.agent.md             # Code review checklist
│   ├── rn-perf.agent.md                 # Performance optimization
│   ├── rn-testing.agent.md              # Test writing specialist
│   └── speckit-designer.agent.md        # Spec Kit — spec-driven development
├── skills/
│   ├── new-component/SKILL.md           # Scaffold a new component
│   ├── new-screen/SKILL.md              # Scaffold a new screen
│   ├── new-hook/SKILL.md                # Scaffold a custom hook
│   ├── spec-to-code/SKILL.md            # Spec Kit workflow (specify → plan → implement)
│   ├── debug-crash/SKILL.md             # Debug a crash or error
│   ├── optimize-perf/SKILL.md           # Fix performance bottlenecks
│   ├── write-tests/SKILL.md             # Write tests for a component/hook
│   └── refactor/SKILL.md               # Refactor code safely
└── README.md                            # This file

.vscode/
├── mcp.json                             # MCP connections (Rovo, DeepWiki, Context7, Playwright)
└── settings.json                        # GHCP features (steering, handoffs, agents)
```

## Setup

### 1. VS Code Settings

The `.vscode/settings.json` enables key GHCP features:

| Setting | What It Does |
|---------|--------------|
| `chat.agent.enabled` | Enables Copilot agent mode |
| `chat.agent.steering.enabled` | Lets you steer Copilot to use specific agents |
| `chat.agent.handoffs.enabled` | Allows handing off plan implementation to another agent |
| `chat.mcp.enabled` | Enables MCP server connections |
| `github.copilot.chat.agent.useProjectAgents` | Discovers workspace agents and skills |
| `github.copilot.chat.codeGeneration.useInstructionFiles` | Loads `.github/copilot-instructions.md` |

### 2. MCP Server Connections

The `.vscode/mcp.json` configures these servers (you'll be prompted for credentials on first use):

| Server | Purpose |
|--------|---------|
| **rovo** | Atlassian Rovo — Jira tickets, Confluence specs, team context |
| **deepwiki** | DeepWiki — open-source library documentation and context |
| **react-native** | Context7 — React Native API docs and examples |
| **playwright** | Playwright — browser automation and E2E testing |

> **Spec Kit** (spec-driven development) is configured separately. See [`docs/speckit-setup.md`](../docs/speckit-setup.md).

#### Rovo (Atlassian)

Uses the unified endpoint `https://mcp.atlassian.com/v1/mcp` with OAuth 2.1. On first connection, a browser-based authorization flow will open automatically — no manual API token needed.

Requires an Atlassian Cloud site with Jira, Compass, and/or Confluence.

Rovo enables Copilot to:
- Search and create Jira issues, Confluence pages, and Compass components
- Pull ticket descriptions, acceptance criteria, and design docs
- Cross-reference content across Atlassian products

## Usage

### Agents

Invoke agents in Copilot Chat with `@agent-name`:

- **@rn-architect** — "Design the navigation structure for a multi-tab app with auth flow"
- **@rn-debugger** — "This crash happens on Android only: `TypeError: undefined is not an object`"
- **@rn-reviewer** — "Review this PR for React Native best practices"
- **@speckit-designer** — "Help me specify the photo album feature using Spec Kit"
- **@rn-perf** — "The home screen takes 3 seconds to render, help me optimize"
- **@rn-testing** — "Write tests for the UserProfile component"

#### Steering & Handoffs

With steering enabled, Copilot can automatically route tasks to the right agent. You can also:
- Ask Copilot to create a plan, then hand off implementation to an agent
- Use `@rn-architect` to plan, then hand off to `@rn-testing` to write tests

### Skills (slash commands)

Type `/` in Copilot Chat to invoke skills:

- **/new-component** — Scaffold a typed component with StyleSheet and accessibility
- **/new-screen** — Create a navigation-typed screen with safe areas
- **/new-hook** — Generate a custom hook with proper cleanup
- **/spec-to-code** — Run the Spec Kit workflow (specify → plan → tasks → implement)
- **/debug-crash** — Structured crash debugging workflow
- **/optimize-perf** — Performance analysis and fix
- **/write-tests** — Generate Jest + RNTL tests
- **/refactor** — Safe refactoring with behavior preservation

Skills are also auto-discovered by agents when relevant — you don't always need to invoke them manually.

## Conventions Enforced

All agents and skills enforce:

- TypeScript strict mode — no `any` types
- Functional components only (no class components)
- `StyleSheet.create` for all styles (no inline styles)
- React Navigation v6+ with typed params
- Accessibility attributes on interactive elements
- Theme tokens for colors, spacing, typography
- Co-located tests with React Native Testing Library
- Secure storage for sensitive data
- HTTPS for all network requests
