---
name: debug-crash
description: 'Diagnose and fix a React Native crash, error, or unexpected behavior across JS, native, and build layers. Use when: app crashes, red screen, build failure, "debug", "crash", "error", "fix bug", "not working".'
argument-hint: 'Error message, platform (iOS/Android), and reproduction steps'
---

# Debug React Native Issue

## When to Use
- App crashes with a red screen or native error
- Build failure (Metro, Gradle, Xcode, CocoaPods)
- Runtime exception or unexpected behavior
- Native module linking issues

## Procedure

1. **Search the codebase** for the error message or related code
2. **Read the relevant files** — component, hook, service, native module
3. **Check common causes**:
   - Missing null checks on navigation params
   - Unmounted component state updates
   - Native module not linked / autolinking failure
   - Incorrect import paths or circular dependencies
   - Metro bundler cache issues
   - Pod install needed (iOS) / Gradle sync needed (Android)
4. **Trace the call stack** from error to root cause
5. **Apply the fix** with minimal changes
6. **Verify** by checking for type errors and logical correctness

## Common Recovery Commands

```bash
# Metro cache
npx react-native start --reset-cache

# iOS pods
cd ios && pod install --repo-update

# Android clean
cd android && ./gradlew clean

# Watchman
watchman watch-del-all
```

## Output Format

1. **Root cause**: Clear explanation of what went wrong
2. **Fix**: The exact code/config change
3. **Prevention**: Recommended guard (lint rule, type, test)
