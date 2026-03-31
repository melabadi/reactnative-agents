---
name: new-screen
description: 'Generate a new React Native screen with typed navigation props, safe area handling, error boundary, and navigator registration. Use when: creating a screen, adding a page, "new screen", "create screen".'
argument-hint: 'Screen name, stack, and route params (e.g., "ProfileScreen on MainStack with { userId: string }")'
---

# New React Native Screen

## When to Use
- Adding a new screen to the app
- Creating a tabbed or stacked page
- Scaffolding a screen from requirements

## Procedure

1. **Create screen file**: `src/screens/<ScreenName>/<ScreenName>.tsx`
2. **Add typed navigation props**: `NativeStackScreenProps<RootStackParamList, 'ScreenName'>`
3. **Wrap with SafeAreaView** or `useSafeAreaInsets`
4. **Add loading and error states** if the screen fetches data
5. **Update navigation types**: Add to `RootStackParamList` in `src/navigation/types.ts`
6. **Register in navigator**: Add `<Stack.Screen>` in the appropriate navigator

## Template

```tsx
import React from 'react';
import { View, StyleSheet } from 'react-native';
import { SafeAreaView } from 'react-native-safe-area-context';
import type { NativeStackScreenProps } from '@react-navigation/native-stack';
import type { RootStackParamList } from '../navigation/types';

type Props = NativeStackScreenProps<RootStackParamList, 'ScreenName'>;

/** Brief screen description */
export const ScreenName: React.FC<Props> = ({ route, navigation }) => {
  return (
    <SafeAreaView style={styles.root}>
      <View style={styles.content}>
        {/* Screen content */}
      </View>
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  root: { flex: 1 },
  content: { flex: 1, padding: 16 },
});
```

## Conventions

- Use `InteractionManager.runAfterInteractions` for post-navigation heavy work
- Use `useFocusEffect` for screen-focus-specific side effects
- Lazy-load with `React.lazy` for infrequently visited screens
