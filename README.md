# aggiemap-e2e-playwright

Primary repository for collaborative Aggiemap E2E Playwright tests

## Prerequisites

- **Node.js**: Version 18.x or higher (tested with v20.19.5)
- **npm**: Version 9.x or higher (tested with v10.8.2)

> **Note**: If you use [nvm](https://github.com/nvm-sh/nvm), you can run `nvm use` to automatically switch to the correct Node version (specified in `.nvmrc`).

You can check your current versions by running:
```bash
node --version
npm --version
```

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/TamuGeoInnovation/aggiemap-e2e-playwright.git
cd aggiemap-e2e-playwright
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Install Playwright Browsers

Playwright requires browser binaries to run tests. Install them using:

```bash
npx playwright install
```

This will download Chromium, Firefox, and WebKit browsers.

If you only need specific browsers, you can install them individually:
```bash
npx playwright install chromium
npx playwright install firefox
npx playwright install webkit
```

### 4. Verify Installation

Run the example tests to verify everything is set up correctly:

```bash
npm test
```

## Running Tests

### Run all tests
```bash
npm test
```

### Run tests in headed mode (with browser UI visible)
```bash
npm run test:headed
```

### Run tests in UI mode (interactive mode with time travel debugging)
```bash
npm run test:ui
```

### Run tests in debug mode
```bash
npm run test:debug
```

### Run tests in a specific browser
```bash
npm run test:chromium
npm run test:firefox
npm run test:webkit
```

### View test report
After running tests, you can view the HTML report:
```bash
npm run report
```

## Writing Tests

Tests are located in the `tests/` directory. Each test file should have the `.spec.ts` extension.

Example test structure:
```typescript
import { test, expect } from '@playwright/test';

test.describe('Feature Name', () => {
  test('should do something', async ({ page }) => {
    await page.goto('https://example.com');
    await expect(page).toHaveTitle(/Expected Title/);
  });
});
```

### Page Object Model

For better test organization and maintainability, consider using the Page Object Model pattern. Page objects are located in `tests/pages/`. See `tests/example-page-object.spec.ts` for an example.

Benefits of Page Object Model:
- Encapsulates page elements and interactions
- Reduces code duplication
- Makes tests easier to maintain
- Improves test readability

## Test Code Generation

Playwright provides a code generator to help you write tests. Run:
```bash
npm run codegen
```

This will open a browser and the Playwright Inspector. Navigate to your application, and Playwright will generate test code as you interact with the page.

## Configuration

The Playwright configuration is defined in `playwright.config.ts`. You can customize:
- Test directory
- Browser projects
- Timeouts
- Reporters
- Base URLs
- And more

## CI/CD Integration

The repository includes a GitHub Actions workflow (`.github/workflows/playwright.yml`) that runs tests automatically on push and pull requests.

The configuration is optimized for CI environments:
- Tests retry automatically on failure (2 retries on CI)
- Tests run sequentially on CI to avoid resource contention
- `test.only` calls will fail the build on CI
- Test reports are saved as artifacts for 30 days

### Viewing CI Test Reports

When tests run in CI, the HTML report is uploaded as an artifact. To view it:
1. Go to the Actions tab in GitHub
2. Click on the workflow run
3. Download the `playwright-report` artifact
4. Extract and open `index.html` in a browser

## Documentation

- [Playwright Documentation](https://playwright.dev/)
- [Playwright Best Practices](https://playwright.dev/docs/best-practices)
- [Playwright API Reference](https://playwright.dev/docs/api/class-playwright)
