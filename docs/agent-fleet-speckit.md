# Agent Fleet Playbook (Spec Kit First)

This playbook turns your existing agents into a coordinated delivery fleet with Spec Kit as the source of truth.

## Goal

- Make agents collaborate in a predictable pipeline instead of one-off prompts
- Keep one shared artifact chain for every feature: constitution -> spec -> plan -> tasks -> code -> tests -> review
- Reduce context loss between agents with explicit handoffs

## Fleet Topology

1. speckit-designer
Purpose: Requirements shaping and artifact generation in Spec Kit.
2. rn-architect
Purpose: App structure and technical decomposition from Spec Kit plan/tasks.
3. implementation agent (default coding agent)
Purpose: Execute tasks in small batches.
4. rn-reviewer
Purpose: Risk-focused review, regressions, accessibility, and conventions.
5. rn-testing
Purpose: Unit/component test coverage and missing scenarios.
6. rn-perf
Purpose: Performance checks for screens, lists, rendering, and memoization.
7. rn-debugger
Purpose: Failure triage if build/tests/runtime fail.

## Standard Flow Per Feature

1. Branch and scope
- Create a short feature branch name.
- Define one feature outcome and non-goals.

2. Spec Kit intake (mandatory)
- Run /speckit.specify with user-centric behavior.
- Run /speckit.clarify to remove ambiguity.
- Run /speckit.plan with React Native stack decisions.
- Run /speckit.tasks to produce atomic tasks.

3. Architecture pass
- Ask @rn-architect to map tasks to files/modules and sequence.
- Ensure navigation typing, safe area handling, accessibility, and theme usage are included.

4. Implementation pass
- Execute tasks in small batches (2-5 tasks each).
- After each batch: typecheck/build/tests before moving on.
- Keep changes aligned with generated tasks; update tasks if scope changes.

5. Quality pass
- @rn-reviewer for behavioral/regression risks.
- @rn-testing for missing tests and flaky assumptions.
- @rn-perf for rendering/list/interaction bottlenecks.

6. Fix and finalize
- If failures happen, route to @rn-debugger with exact logs and changed files.
- Re-run checks and close open review points.

## Handoff Contract (Use Between Agents)

Use this exact structure when handing work from one agent to another.

Feature ID: <short-id>
Stage: <spec|plan|tasks|implement|review|test|perf|debug>
Objective: <single clear objective>
Inputs:
- Spec artifacts: <paths>
- Changed files: <paths>
- Constraints: <strict mode, no inline styles, typed nav, etc>
Deliverables:
- Required output format
- Required file updates
Done Criteria:
- Behavioral criteria
- Verification criteria (tests/build/lint)
Risks to Watch:
- Known edge cases and regressions

## Copy/Paste Prompt Templates

### 1) Kickoff (Spec Kit)

@speckit-designer
Create feature artifacts for: <feature description>
Run: /speckit.specify, /speckit.clarify, /speckit.plan, /speckit.tasks
Constraints: React Native + TypeScript strict, typed navigation, StyleSheet.create, accessibility labels/roles, theme tokens.
Return:
- Final scope summary
- Open decisions
- Ordered tasks grouped by implementation batches

### 2) Architecture from Tasks

@rn-architect
Using current Spec Kit plan/tasks, produce an implementation map.
Return:
- File-by-file change plan
- Task-to-file mapping
- Risk list and mitigation
- Suggested execution order

### 3) Batch Implementation

Implement only batch <N> from tasks.
Rules:
- Do not expand scope beyond selected tasks.
- Keep APIs and naming consistent.
- Add/update tests for changed behavior.
Return:
- Completed task IDs
- Files changed
- Validation results
- Remaining blockers

### 4) Review Pass

@rn-reviewer
Review the latest changes with focus on regressions, accessibility, typed navigation, and React Native conventions.
Return findings ordered by severity with precise file references.

### 5) Test Pass

@rn-testing
Add missing tests for the implemented tasks and edge cases.
Prefer role-based queries and stable assertions.
Return:
- New/updated tests
- Coverage gaps that still remain

### 6) Perf Pass

@rn-perf
Assess the changed surfaces for rendering and interaction performance risks.
Return:
- Bottlenecks
- Concrete fixes
- Quick verification checklist

### 7) Debug Fallback

@rn-debugger
Investigate failing checks/crash with these logs and changed files: <paste>
Return root cause, minimal fix, and confidence level.

## Fleet Operating Rules

- One coordinator owns final merge decisions.
- One source of truth for requirements: Spec Kit artifacts.
- No implementation starts before tasks exist.
- Every stage emits structured output using the handoff contract.
- Keep batches small to reduce merge and context conflicts.

## Suggested Repo Routine

1. Start every feature with the Spec Kit sequence.
2. Run architecture mapping before first code edit.
3. Implement in batches with immediate validation.
4. Gate merge on reviewer + testing feedback.
5. Run perf pass on UI-heavy features before merge.

## Where This Fits

- Spec Kit setup and commands: docs/speckit-setup.md
- Copilot agents and skills inventory: .github/README.md
