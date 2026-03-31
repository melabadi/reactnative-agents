---
name: spec-to-code
description: 'Run the Spec Kit spec-driven development workflow — from specification to implementation. Use when: "speckit", "spec-driven", "spec to code", "from spec", "specify", "constitution", "implementation plan".'
argument-hint: 'Feature description (e.g., "Build a photo album organizer with drag-and-drop")'
---

# Spec Kit — Spec-Driven Development

## When to Use
- Starting a new feature from requirements
- Converting a product brief into an implementation plan
- Running the full specify → plan → tasks → implement workflow
- Creating or updating the project constitution

## Prerequisites

Ensure Spec Kit is initialized (see `docs/speckit-setup.md`):
```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z
specify init --here --ai copilot
```

## Procedure

1. **Constitution** (one-time per repo):
   - Run `/speckit.constitution` to define project principles
   - Include React Native conventions: functional components, TypeScript strict, StyleSheet, accessibility, theme tokens

2. **Specify** — describe the feature:
   - Run `/speckit.specify` with a user-centric description
   - Focus on the **what and why**, not tech stack details
   - Example: "Build a photo album app where albums are grouped by date and can be reordered by drag-and-drop"

3. **Clarify** (optional but recommended):
   - Run `/speckit.clarify` to surface ambiguities
   - Answer the generated questions to tighten the spec

4. **Plan** — add technical decisions:
   - Run `/speckit.plan` with tech stack: React Native, TypeScript, React Navigation, Zustand
   - Reference `src/theme/` for design tokens

5. **Analyze** (optional):
   - Run `/speckit.analyze` to cross-check spec ↔ plan consistency

6. **Tasks** — generate the work breakdown:
   - Run `/speckit.tasks` to create atomic, testable tasks

7. **Implement** — execute:
   - Run `/speckit.implement` to build the feature

## Output

Spec Kit generates artifacts under `.specify/` in the feature branch:
- `constitution.md` — project principles
- `spec.md` — feature specification
- `plan.md` — technical implementation plan
- `tasks.md` — task breakdown

## Tips

- Keep specs technology-agnostic — the plan step is where you add stack details
- Use `/speckit.checklist` to generate quality validation checklists
- Specs are version-controlled — review them in PRs alongside code
