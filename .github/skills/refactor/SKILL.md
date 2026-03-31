---
name: refactor
description: 'Refactor React Native code to improve structure, readability, and maintainability while preserving behavior. Use when: extracting hooks, splitting components, removing duplication, "refactor", "clean up", "restructure", "extract".'
argument-hint: 'File(s) to refactor and goal (e.g., "src/screens/Home.tsx - extract data fetching into a hook")'
---

# Refactor React Native Code

## When to Use
- Extracting logic from a large component into a hook
- Splitting a monolithic component into smaller pieces
- Removing duplicated code patterns
- Improving type safety (replacing `any` types)
- Simplifying complex conditional rendering

## Procedure

1. **Read the target file(s)** and understand current behavior
2. **Identify the refactoring pattern** to apply (see below)
3. **Apply incremental changes** — small, verifiable steps
4. **Verify behavior is preserved** — no new features, no changed API

## Common Refactoring Patterns

### Extract Custom Hook
- Move stateful logic from a component into `src/hooks/useXxx.ts`
- Keep the component focused on rendering

### Split Component
- Break into smaller focused components
- Use composition over configuration
- Co-locate sub-components if single-use

### Simplify Conditional Rendering
- Replace complex ternary chains with early returns
- Use guard clauses for loading/error states

### Consolidate Duplicates
- Extract shared logic into a utility or hook
- Create a shared component for repeated UI patterns

### Improve Type Safety
- Replace `any` with proper TypeScript types
- Add discriminated unions for complex state

## Rules

1. **Preserve behavior**: Must work identically after refactoring
2. **No feature additions**: Structure only, not new features
3. **Incremental**: Small verifiable changes, not full rewrites
4. **Follow conventions**: All changes follow project coding conventions
