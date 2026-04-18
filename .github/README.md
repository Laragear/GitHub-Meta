# How to call the PHP Testing Workflow:

```yaml
on:
  push:
    branches:
      - "*.x"                               # Only run when pushing to a core branch.
  pull_request:
    types: [opened, synchronize, reopened]  # Only run on PRs.

jobs:
  test:
    name: Testing under PHP 8.5 and PHPUnit
    uses: Laragear/GitHub-Meta/.github/workflows/test-php-8.5-phpunit.yml@main
    with:
      laravel_constraint_min: "12.*"    # or "^12.29", "^12.38", whichever is needed.
    # export_expected: true             # defaults to `LICENSE.md,README.md,composer.json`.
    secrets: inherit                    # required to pass org-wide secrets.
```

# How to call the issue orchestrator

```yaml
on:
  issues:
    types: [opened, edited]             # Trigger the workflow only on issues.

jobs:
  handle-issue:
    uses: Laragear/GitHub-Meta/.github/workflows/manage-issue.yml@main
    with:
      target-org: 'Laragear'
      # log-level: 'verbose'            # Only required if you need debugging.
```

# How to add `dependabot`

```yaml
version: 2
updates:
- package-ecosystem: "composer"
  directory: "/"
  schedule:
    interval: "daily"
    time: "09:00"
    timezone: "America/Santiago"
  open-pull-requests-limit: 2
  groups:
    php-dependencies:
      patterns:
        - "*" # Groups all action updates into one PR to avoid noise
```
