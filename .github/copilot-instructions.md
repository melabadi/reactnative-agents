# React Native Toolkit — Copilot Instructions

## Project Context

This is a **React Native** project. All code generation, refactoring, debugging, and review should follow React Native conventions and the patterns established in this repository.

## Language & Runtime

- **Language**: TypeScript (strict mode)
- **Runtime**: React Native (Hermes engine)
- **Package manager**: Yarn or npm (check `yarn.lock` / `package-lock.json`)
- **Navigation**: React Navigation v6+
- **State management**: Zustand or React Context (check existing patterns)
- **Styling**: StyleSheet.create or styled-components/native

## Coding Conventions

### Naming

- Components: `PascalCase` — file and export name must match
- Hooks: `useCamelCase`
- Utilities/helpers: `camelCase`
- Constants: `UPPER_SNAKE_CASE`
- Types/Interfaces: `PascalCase`, prefixed with `I` for interfaces only when disambiguating
- Variables: lowerCamelCase, max 11 characters where practical

### File Organisation

```
src/
  components/    # Reusable UI components
  screens/       # Screen-level components
  hooks/         # Custom hooks
  navigation/    # Navigation stacks & config
  services/      # API & external service layers
  stores/        # State management
  utils/         # Pure utility functions
  types/         # Shared TypeScript types
  assets/        # Images, fonts, animations
  constants/     # App-wide constants
  theme/         # Colors, typography, spacing tokens
```

### Component Pattern

Always use **functional components** with hooks. Never use class components.

```tsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

interface Props {
  title: string;
}

export const MyComponent: React.FC<Props> = ({ title }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>{title}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1 },
  title: { fontSize: 16, fontWeight: '600' },
});
```

### Hooks Pattern

```tsx
import { useState, useCallback } from 'react';

export const useToggle = (init = false) => {
  const [val, setVal] = useState(init);
  const toggle = useCallback(() => setVal((v) => !v), []);
  return [val, toggle] as const;
};
```

## React Native Best Practices

1. **Avoid inline styles** — always use `StyleSheet.create`
2. **Memoize expensive computations** — use `useMemo` and `useCallback` appropriately
3. **FlatList over ScrollView** for long lists — always provide `keyExtractor`
4. **Avoid anonymous functions in JSX** for lists and frequently re-rendered components
5. **Use `React.memo`** for pure presentational components receiving complex props
6. **Platform-specific code** — use `Platform.select` or `.ios.tsx` / `.android.tsx` suffixes
7. **Safe area handling** — always use `SafeAreaView` or `useSafeAreaInsets`
8. **Accessibility** — include `accessibilityLabel`, `accessibilityRole`, and `accessibilityHint` on interactive elements
9. **Error boundaries** — wrap screen-level components
10. **Image optimization** — use `FastImage` for network images, provide `width`/`height`

## Navigation

- Use typed navigation with `NativeStackScreenProps` or `CompositeScreenProps`
- Define a central `RootStackParamList` type
- Deep linking config should live in `src/navigation/linking.ts`

## Testing

- Unit tests: Jest + React Native Testing Library
- Test files: co-located as `__tests__/ComponentName.test.tsx` or `ComponentName.test.tsx`
- Prefer `getByRole`, `getByText`, `getByTestId` (in that priority order)
- Mock native modules in `jest.setup.js`

## Security

- Never hardcode API keys or secrets — use environment variables via `react-native-config`
- Validate all external input before rendering
- Use HTTPS for all network requests
- Sanitize deep link parameters
- Store sensitive data in secure storage (`react-native-keychain`)

## Performance

- Profile with Flipper and React DevTools
- Monitor JS thread frame rate — keep above 60fps
- Use `InteractionManager.runAfterInteractions` for expensive post-navigation work
- Lazy-load screens with `React.lazy` + `Suspense` or navigation lazy loading
- Avoid large re-renders — split components and lift state only as needed

## Spec Kit (Spec-Driven Development)

This project uses [Spec Kit](https://github.com/github/spec-kit) for spec-driven development:
- Run `specify init --here --ai copilot` to bootstrap Spec Kit in this repo
- Use `/speckit.constitution` to define project principles before coding
- Use `/speckit.specify` → `/speckit.plan` → `/speckit.tasks` → `/speckit.implement` workflow
- Specifications live in the feature branch under the `.specify/` directory
- See `docs/speckit-setup.md` for full setup and usage instructions

## Documentation

- Every exported component/hook should have a brief JSDoc comment
- README files in feature directories for complex modules
- Storybook stories for shared UI components when applicable
