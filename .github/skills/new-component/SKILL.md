---
name: new-component
description: 'Generate a new React Native functional component with TypeScript, StyleSheet, props interface, accessibility, and barrel export. Use when: creating a component, scaffolding UI, "new component", "create component".'
argument-hint: 'Component name and brief description (e.g., "AvatarBadge - circular user avatar with status indicator")'
---

# New React Native Component

## When to Use
- Creating a new reusable UI component
- Scaffolding a component from a design spec
- Adding a new presentational or container component

## Procedure

1. **Determine location**: `src/components/<ComponentName>/<ComponentName>.tsx`
2. **Create the component file** with:
   - `Props` interface with typed props
   - `React.FC<Props>` functional component (never class components)
   - `StyleSheet.create` for all styles (no inline styles)
   - Theme tokens from `src/theme/` for colors, spacing, typography
   - Accessibility attributes (`accessibilityLabel`, `accessibilityRole`)
   - JSDoc comment on the exported component
3. **Create barrel export**: `src/components/<ComponentName>/index.ts`
4. **Add `React.memo`** if the component is purely presentational with complex props

## Template

```tsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

interface Props {
  /** Brief prop description */
  title: string;
}

/** Brief component description */
export const ComponentName: React.FC<Props> = ({ title }) => {
  return (
    <View style={styles.root} accessibilityRole="summary">
      <Text style={styles.title}>{title}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  root: { flex: 1 },
  title: { fontSize: 16, fontWeight: '600' },
});
```

## Conventions

- File and export name in PascalCase — must match
- Variables in lowerCamelCase, max 11 characters
- Use `useSafeAreaInsets` if the component touches screen edges
- Export the Props interface for consumer type safety
