# Project setup notes

This project follows the supplied Web Project assessment and structure notes.

## Assessment workflow

1. Register a new user.
2. Select the group **Do Not Use**.
3. Generate unique user details for each run.
4. Use an existing administrator account to approve the new user.
5. Use an administrator account to promote the new user to administrator.
6. Log in as the newly created user.
7. Verify that login succeeded.
8. Verify that the user has the administrator role.

## Required technical approach

- Playwright
- Page Object Model (POM)
- GitHub repository
- GitHub Actions CI/CD
- Allure report

## Local prerequisites

- Node.js (use an active LTS release; Node.js 22 is a suitable baseline)
- npm (bundled with Node.js)
- Git
- IntelliJ IDEA or another editor
- Java is not required when using the locally installed Allure Report 3 npm CLI. It may be needed for other Allure CLI installation routes.

## Initialise the project

From the repository root:

```bash
npm init playwright@latest
```

Choose TypeScript and the `tests` folder. Add a GitHub Actions workflow when prompted if one is not already present. Then install the Allure integration and local Allure Report 3 CLI:

```bash
npm install -D allure-playwright allure
```

The Playwright initializer installs `@playwright/test`, creates the Playwright configuration and TypeScript setup, and can install browser binaries. Commit the generated `package-lock.json` so CI can use reproducible `npm ci` installs.

## Allure setup

Configure Allure alongside the standard Playwright reporter in `playwright.config.ts`:

```ts
reporter: [
  ['list'],
  ['allure-playwright', { resultsDir: 'allure-results' }],
],
```

Run tests and generate/open the report:

```bash
npx playwright test
npx allure generate allure-results --clean
npx allure open allure-report
```

Use `npx allure serve allure-results` for a one-command local preview if preferred.

## Configuration and secrets

Store the application base URL and test account credentials in environment variables or GitHub Actions repository secrets. Do not commit real credentials or a populated local `.env` file. Keep a sanitized `.env.example` file containing variable names and placeholder values only.

The actual application URL, administrator credentials, registration fields, and approval/role-management UI are not specified in the supplied assessment notes. Confirm these against the target application before implementing page objects.

## CI schedule

GitHub Actions cron schedules are expressed in UTC. South Africa Standard Time is UTC+2, so 22:00 UTC corresponds to 00:00 the next day in South Africa:

```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 22 * * *'
  workflow_dispatch:
```

Scheduled workflows should be committed to the repository's default branch. Confirm the schedule on the Actions tab after the workflow is pushed. GitHub may delay scheduled runs during periods of high load, so check the actual run history.

## CI workflow outline

The workflow should check out the repository, set up the chosen Node.js LTS version, run `npm ci`, install Playwright browsers and OS dependencies with `npx playwright install --with-deps`, run the tests, and upload the Playwright and Allure result folders as artifacts even when tests fail.

Use one worker in CI initially to improve repeatability. Add secrets for environment-specific credentials in GitHub repository settings rather than hardcoding them in YAML.

## Evidence and reporting

- Capture screenshots for important checkpoints and on test failure.
- Attach useful screenshots and traces to Allure results.
- Upload `allure-results`, `playwright-report`, and relevant screenshots as workflow artifacts.
- Do not commit generated report output unless the assessment explicitly requires it; retain it as CI artifacts instead.

## Suggested source layout

```text
.github/
  workflows/
    playwright.yml
pages/
tests/
fixtures/
utils/
docs/
  PROJECT_SETUP.md
.env.example
.gitignore
package.json
package-lock.json
playwright.config.ts
tsconfig.json
README.md
```

The concrete page classes and test fixture names should be finalized after inspecting the target application's screens and selectors.
