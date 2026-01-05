# QA Automation Pipeline

A comprehensive CI/CD pipeline for automated testing that runs on every push, pull request, and daily at 2 AM UTC.

## Overview

This repository contains a complete QA automation setup using GitHub Actions, featuring end-to-end testing, API testing, Selenium WebDriver tests, code quality checks, test coverage reports, and performance testing.

## Features

- **Cypress E2E Tests** - Cross-browser testing on Chrome and Firefox
- **API Tests** - Automated API testing using Newman (Postman)
- **Selenium WebDriver Tests** - Java-based browser automation
- **Code Quality Checks** - ESLint and Prettier integration
- **Test Coverage Reports** - Automated coverage reporting with Codecov
- **Performance Testing** - Load testing with k6
- **Slack Notifications** - Real-time alerts on test failures

## Pipeline Jobs

### 1. Cypress E2E Tests
Runs end-to-end tests across multiple browsers with automatic screenshot and video capture on failures.

### 2. API Tests (Newman)
Executes Postman collections to validate API endpoints and generates HTML reports.

### 3. Selenium WebDriver Tests
Runs Java-based Selenium tests with Chrome and ChromeDriver setup.

### 4. Code Quality & Linting
Performs code quality checks using ESLint and Prettier to maintain code standards.

### 5. Test Coverage Report
Generates comprehensive test coverage reports and uploads to Codecov.

### 6. Performance Tests
Conducts load testing using k6 to ensure application performance under stress.

### 7. Notifications
Sends Slack notifications when tests fail to keep the team informed.

## Prerequisites

Before running this pipeline, ensure your repository contains:

- `package.json` with npm scripts for testing
- `cypress.config.js` for Cypress configuration
- `postman-collections/api-tests.json` for API tests
- Java project with Maven for Selenium tests
- Performance test scripts in `performance-tests/`

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/Kofiahorlu583/tekk.git
cd tekk
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Secrets
Add the following secrets to your GitHub repository (Settings → Secrets and variables → Actions):

- `SLACK_WEBHOOK_URL` - Your Slack webhook URL for notifications

### 4. Project Structure
```
.
├── .github/
│   └── workflows/
│       └── qa-automation.yml
├── cypress/
│   ├── e2e/
│   ├── fixtures/
│   └── support/
├── postman-collections/
│   └── api-tests.json
├── performance-tests/
│   └── load-test.js
├── src/
├── tests/
└── package.json
```

## Triggering the Pipeline

The pipeline automatically runs on:
- Push to `main` or `develop` branches
- Pull requests to `main` or `develop` branches
- Daily at 2:00 AM UTC (scheduled)

### Manual Trigger
You can also trigger the workflow manually from the GitHub Actions tab.

## Viewing Test Results

### Artifacts
Test artifacts are automatically uploaded and retained:
- **Cypress screenshots** (7 days) - Available on test failures
- **Cypress videos** (7 days) - Available for all test runs
- **API test reports** (30 days) - HTML reports with detailed results
- **Selenium test results** (30 days) - JUnit XML reports
- **k6 performance results** (30 days) - Load test metrics

### Accessing Artifacts
1. Go to the Actions tab in your GitHub repository
2. Click on a workflow run
3. Scroll down to the "Artifacts" section
4. Download the desired artifact

## Local Development

### Running Tests Locally

**Cypress Tests:**
```bash
npm run cypress:open  # Interactive mode
npm run cypress:run   # Headless mode
```

**API Tests:**
```bash
newman run postman-collections/api-tests.json
```

**Selenium Tests:**
```bash
mvn clean test
```

**Performance Tests:**
```bash
k6 run performance-tests/load-test.js
```

**Code Quality:**
```bash
npm run lint
npm run format:check
```

## Configuration

### Customizing Test Browsers
Edit the browser matrix in `.github/workflows/qa-automation.yml`:
```yaml
strategy:
  matrix:
    browser: [chrome, firefox, edge]
```

### Adjusting Node.js Version
Change the Node.js version in the workflow:
```yaml
- name: Setup Node.js
  uses: actions/setup-node@v3
  with:
    node-version: '20'  # Change to desired version
```

### Modifying Retention Days
Adjust artifact retention periods:
```yaml
retention-days: 14  # Change as needed
```

## Troubleshooting

### Common Issues

**Issue: Cypress tests failing**
- Check that `cypress.config.js` exists
- Verify test files are in the correct directory
- Review screenshots and videos in artifacts

**Issue: API tests failing**
- Ensure `postman-collections/api-tests.json` exists
- Verify API endpoints are accessible
- Check environment variables

**Issue: Selenium tests failing**
- Confirm Maven project structure is correct
- Verify Java version compatibility
- Check ChromeDriver installation

**Issue: Pipeline not triggering**
- Verify the workflow file is in `.github/workflows/`
- Check branch names match your repository
- Ensure GitHub Actions is enabled

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Best Practices

- Write clear, descriptive test names
- Keep tests independent and isolated
- Use fixtures for test data
- Maintain test documentation
- Review test reports regularly
- Fix failing tests promptly

## Support

For issues or questions:
- Open an issue in this repository
- Check the GitHub Actions logs
- Review test artifacts for detailed error information

## License

This project is licensed under the MIT License.

## Authors

- **Sterling Dwiip** - [Kofiahorlu583](https://github.com/Kofiahorlu583)

## Acknowledgments

- GitHub Actions for CI/CD automation
- Cypress for E2E testing
- Newman for API testing
- Selenium for browser automation
- k6 for performance testing

---

**Built with ❤️ for Quality Assurance**
