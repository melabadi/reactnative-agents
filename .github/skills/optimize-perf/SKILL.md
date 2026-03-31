---
name: optimize-perf
description: 'Analyze and optimize React Native performance — rendering, JS thread, animations, lists, and startup time. Use when: slow rendering, janky scrolling, frame drops, "performance", "optimize", "slow", "jank", "lag".'
argument-hint: 'Performance area and symptom (e.g., "FlatList janky scrolling on HomeScreen")'
---

# Optimize React Native Performance

## When to Use
- Janky scrolling or frame drops
- Slow screen transitions or startup
- High memory usage or leaks
- Sluggish animations

## Procedure

1. **Read the target component/screen** and its dependencies
2. **Identify anti-patterns**:
   - Inline styles (should use `StyleSheet.create`)
   - Anonymous functions in JSX render
   - Missing `keyExtractor` or wrong key in lists
   - Missing `React.memo` on presentational components
   - Unnecessary state in parent causing child re-renders
   - Heavy computation in render without `useMemo`
   - Animated API without `useNativeDriver: true`
3. **Check list configuration** (if FlatList):
   - `windowSize`, `maxToRenderPerBatch`, `initialNumToRender`
   - `getItemLayout` for fixed-height items
   - `removeClippedSubviews` for long lists
4. **Check navigation performance**:
   - Lazy screen loading
   - `InteractionManager.runAfterInteractions` for post-navigation work
5. **Apply targeted optimizations**

## Optimization Priority

1. Fix the single biggest bottleneck first
2. Measure improvement after each change
3. Avoid premature optimization — only optimize what's measurably slow

## Output Format

For each optimization:
1. What was slow and why
2. The specific code change
3. Expected improvement
4. Any trade-offs
