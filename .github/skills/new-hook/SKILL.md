---
name: new-hook
description: 'Generate a new custom React hook with TypeScript, proper cleanup, stable return references, and JSDoc. Use when: creating a hook, extracting logic, "new hook", "create hook", "custom hook".'
argument-hint: 'Hook name and purpose (e.g., "useDebounce - debounces a value with configurable delay")'
---

# New Custom Hook

## When to Use
- Extracting stateful logic from a component
- Creating a reusable behavior pattern
- Encapsulating side effects with proper cleanup

## Procedure

1. **Create hook file**: `src/hooks/<hookName>.ts`
2. **Name with `use` prefix**: `useCamelCase`
3. **Type all parameters and return values**
4. **Add proper cleanup** in `useEffect` returns
5. **Wrap callbacks** in `useCallback` for reference stability
6. **Export the return type** for consumer type safety
7. **Add JSDoc** on the exported hook

## Template

```tsx
import { useState, useCallback, useEffect } from 'react';

/** Brief hook description */
export const useMyHook = (param: ParamType) => {
  const [state, setState] = useState<StateType>(initialValue);

  const action = useCallback(() => {
    // logic
  }, [/* deps */]);

  useEffect(() => {
    // setup
    return () => {
      // cleanup — unsubscribe, clear timers, etc.
    };
  }, [/* deps */]);

  return { state, action } as const;
};
```

## Conventions

- Never return unstable references — wrap in `useCallback`
- Use `as const` for tuple returns
- Document edge cases in JSDoc
- Place in `src/hooks/` with barrel `index.ts` export
