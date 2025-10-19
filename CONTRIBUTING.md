# Contributing to Aggiemap E2E Playwright Tests

Thank you for your interest in contributing to the Aggiemap E2E test suite!

## Getting Started

1. Follow the setup instructions in the [README.md](README.md)
2. Make sure all tests pass before making changes
3. Create a new branch for your work

## Writing Tests

### Test Organization

- Place tests in the `tests/` directory
- Use descriptive names for test files: `feature-name.spec.ts`
- Group related tests using `test.describe()`

### Test Best Practices

1. **Use Page Objects**: For complex pages, consider using the Page Object Model
2. **Keep tests isolated**: Each test should be independent
3. **Use meaningful assertions**: Make it clear what you're testing
4. **Avoid hardcoded waits**: Use Playwright's auto-waiting features
5. **Clean up after tests**: Use `beforeEach` and `afterEach` hooks

### Example Test Structure

```typescript
import { test, expect } from '@playwright/test';

test.describe('Feature Name', () => {
  test.beforeEach(async ({ page }) => {
    // Setup code
    await page.goto('/feature');
  });

  test('should display correct title', async ({ page }) => {
    await expect(page).toHaveTitle(/Expected Title/);
  });

  test('should handle user interaction', async ({ page }) => {
    await page.click('button#submit');
    await expect(page.locator('.success-message')).toBeVisible();
  });
});
```

## Running Tests Locally

### Before submitting a PR

```bash
# Run all tests
npm test

# Run tests in UI mode for debugging
npm run test:ui

# Check TypeScript types
npx tsc --noEmit
```

## Pull Request Process

1. Create a feature branch from `main`
2. Write your tests following the guidelines above
3. Ensure all tests pass locally
4. Create a pull request with a clear description
5. Wait for CI/CD checks to pass
6. Request review from maintainers

## Debugging Tests

### UI Mode (Recommended)
```bash
npm run test:ui
```

### Debug Mode
```bash
npm run test:debug
```

### View Test Traces
When tests fail in CI, download the artifacts and view traces:
```bash
npx playwright show-trace path/to/trace.zip
```

## Code Style

- Use TypeScript for all test files
- Follow existing code formatting
- Use meaningful variable and function names
- Add comments for complex test logic

## Questions?

If you have questions, please open an issue on GitHub.
