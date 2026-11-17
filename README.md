# Playwright User Management Automation

## Project Overview

This project implements automated end-to-end testing of a web application's user management functionality using **Playwright, TypeScript and the Page Object Model (POM)** design pattern.

The automation covers user registration, administrator approval, role assignment, login verification and administrator role validation.

## Technology Stack

| Technology | Purpose |
|---|---|
| Playwright | Web UI automation |
| TypeScript | Programming language |
| Node.js | JavaScript runtime |
| Page Object Model | Test automation design pattern |
| GitHub | Source code management |
| GitHub Actions | CI/CD pipeline |
| Allure | Test reporting |

## Project Prerequisites

Install the following before setting up the project:

1. **Node.js 22 LTS or compatible supported version**
   - https://nodejs.org/
2. **Git**
   - https://git-scm.com/
3. **IntelliJ IDE**
   - https://www.jetbrains.com/
4. **GitHub account**
   - https://github.com/
5. **Java** (if required by the selected Allure CLI installation).

## Repository Setup

Clone the repository:

```bash
git clone https://github.com/ZuzekaL/playwright-user-management-automation.git
```

Navigate into the project:

```bash
cd playwright-user-management-automation
```

Install project dependencies:

```bash
npm install
```

Install Playwright browsers:

```bash
npx playwright install
```

## Dependencies

The project uses the following development dependencies:

- `@playwright/test` - Playwright test framework.
- `typescript` - TypeScript support.
- `@types/node` - Node.js type definitions.
- `allure-playwright` - Allure integration for Playwright.
- `allure` - Allure Report 3 CLI.

Install the dependencies:

```bash
npm install -D @playwright/test typescript @types/node allure-playwright allure
```

## Project Structure

```text
playwright-user-management-automation/
│
├── .github/
│   └── workflows/
│       └── playwright.yml
│
├── pages/
│   ├── RegistrationPage.ts
│   ├── LoginPage.ts
│   ├── AdminPage.ts
│   └── DashboardPage.ts
│
├── tests/
│   └── user-management.spec.ts
│
├── fixtures/
│   └── test-fixtures.ts
│
├── utils/
│   └── test-data.ts
│
├── screenshots/
│
├── allure-results/
│
├── allure-report/
│
├── .env.example
├── .gitignore
├── package.json          # Dependencies and scripts
├── package-lock.json
├── playwright.config.ts  # Playwright configuration
├── tsconfig.json         # TypeScript configuration
└── README.md             # This file
```

## Test Scenarios

The automation will cover the following workflow:

1. Register a new user.
2. Ensure all registration details are unique.
3. Select the group "Do Not Use".
4. Approve the newly registered user using an existing administrator account.
5. Assign administrator privileges to the newly registered user.
6. Log in using the newly created account.
7. Verify successful login.
8. Verify that the logged-in user has administrator privileges.

## Running the Tests

Run all tests:

```bash
npx playwright test
```

Run tests in headed mode:

```bash
npx playwright test --headed
```
Run tests in UI mode (interactive)

```bash
npm run test:ui
```

# Run tests in specific browser
npm run test:chrome      # Chromium only
npm run test:firefox     # Firefox only
npm run test:webkit      # Safari only

Run a specific test file:

```bash
npx playwright test tests/user-management.spec.ts
```

## Allure Reporting

Generate the Allure report:

```bash
npx allure generate allure-results --clean -o allure-report
```

Open the report:

```bash
npx allure open allure-report
```

## CI/CD Pipeline

GitHub Actions will automatically execute the Playwright test suite:

- On every push to the repository.
- On pull requests.
- Daily at 00:00 South African Standard Time (SAST).

The pipeline will install dependencies, install browser requirements, execute the tests and retain the test reports and relevant screenshots as build artifacts.

## Test Evidence

Screenshots will be captured to provide evidence of test execution, including successful and failed scenarios where applicable.

Allure reports will provide detailed test execution results, including test status, execution steps and attachments.

## Configuration

Application URLs and test account credentials will be configured through environment variables.

Sensitive credentials must never be committed to the repository.

## Author

QA Automation Project – Zuzeka Leso

## License

This project demonstrates end-to-end web application testing using Playwright, TypeScript, and the Page Object Model (POM) design pattern, focusing on user registration, administrative approval, role management, and authentication verification.
