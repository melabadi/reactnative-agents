---
name: write-tests
description: 'Write comprehensive tests for a React Native component or hook using Jest and React Native Testing Library. Use when: writing tests, adding test coverage, "test", "write tests", "unit test", "component test".'
argument-hint: 'File to test and test type (e.g., "src/components/Button/Button.tsx component test")'
---

# Write React Native Tests

## When to Use
- Adding tests for a new or existing component
- Testing a custom hook
- Covering a service or utility function

## Procedure

1. **Read the target file** to understand its API, props, states, and behavior
2. **Read related files** (types, hooks, services it depends on)
3. **Create test file** at `__tests__/<TargetName>.test.tsx` (co-located)
4. **Write tests covering**:

### For Components
- Renders correctly with required props
- Renders each visual variant/state
- User interactions trigger correct callbacks
- Conditional rendering based on props
- Accessibility attributes are present
- Edge cases (empty data, error states, loading states)

### For Hooks
- Initial state is correct
- State transitions work as expected
- Cleanup runs on unmount
- Edge cases and return value stability

### For Services/Utils
- Happy path with valid inputs
- Edge cases and boundary values
- Error handling paths

## Testing Conventions

- Query priority: `getByRole` > `getByText` > `getByTestId`
- Use `fireEvent` for user interactions
- Use `waitFor` for async operations
- Mock native modules in `jest.setup.js`
- Each test is independent — no shared mutable state
- Test names describe user behavior: "displays error message when submission fails"

## Template

```tsx
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react-native';
import { MyComponent } from '../MyComponent';

describe('MyComponent', () => {
  it('renders the title', () => {
    render(<MyComponent title="Hello" />);
    expect(screen.getByText('Hello')).toBeTruthy();
  });

  it('calls onPress when tapped', () => {
    const onPress = jest.fn();
    render(<MyComponent onPress={onPress} title="Tap" />);
    fireEvent.press(screen.getByRole('button'));
    expect(onPress).toHaveBeenCalledTimes(1);
  });
});
```
