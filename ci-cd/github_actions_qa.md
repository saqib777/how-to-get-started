# GitHub Actions for QA — Complete Guide

How to automatically run your tests on every push using GitHub Actions.
No servers to maintain — completely free for public repos.

---

## What is CI/CD?

CI = Continuous Integration. Every time you push code,
your tests run automatically and you get instant feedback.
If tests fail, you know before it reaches production.

---

## Your First Workflow

Create this file in your repo:
`.github/workflows/tests.yml`

```yaml
name: Run Tests

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run tests
        run: pytest -v --tb=short
```

Push this file to GitHub. Every future push will run your tests automatically.

---

## Adding an HTML Report

```yaml
      - name: Run tests with report
        run: |
          pytest -v --tb=short \
            --html=reports/report.html \
            --self-contained-html

      - name: Upload report
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: test-report
          path: reports/report.html
```

`if: always()` means the report uploads even when tests fail.
Download it from the Actions tab on GitHub after each run.

---

## Matrix Testing — Multiple Python Versions

```yaml
    strategy:
      matrix:
        python-version: ['3.10', '3.11', '3.12']

    steps:
      - uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
```

This runs your tests on all three versions simultaneously.

---

## Environment Variables and Secrets

Never hardcode credentials. Use GitHub Secrets:

1. Go to repo → Settings → Secrets → Actions
2. Add `API_KEY`, `BASE_URL`, etc.
3. Use in workflow:

```yaml
      - name: Run tests
        run: pytest -v
        env:
          API_KEY: ${{ secrets.API_KEY }}
          BASE_URL: ${{ secrets.BASE_URL }}
```

---

## Status Badge

Add this to your README to show test status:

```markdown
![Tests](https://github.com/saqib777/dsa-journal/actions/workflows/run_tests.yml/badge.svg)
```

---

## Common Triggers

```yaml
on:
  push:                          # every push
  pull_request:                  # every PR
  schedule:
    - cron: '0 6 * * *'         # daily at 6 AM UTC
  workflow_dispatch:             # manual trigger from GitHub UI
```

---

## Debugging Failed Runs

1. Click **Actions** tab on GitHub
2. Click the failed run
3. Expand the failed step to see the full output
4. Download artifacts (screenshots, reports) if configured

Common failures:
- Missing `requirements.txt` — run `pip freeze > requirements.txt` locally
- Import errors — check your module paths
- Timeout — add `timeout-minutes: 10` to the job
