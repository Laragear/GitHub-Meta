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
    name: Testing with PHPUnit
    uses: Laragear/GitHub-Meta/.github/workflows/test-php-8.5-phpunit.yml@main
    with:
      # Optional: Override the default PHP versions (Defaults to '["8.3", "8.4", "8.5"]')
      # php_versions: '["8.4", "8.5"]'
      
      # Optional: Override the default Laravel versions (Defaults to '["12.*", "13.*"]')
      # laravel_versions: '["13.*"]' 
      
      # Optional: Override exported files check (Defaults to 'LICENSE.md,README.md,composer.json')
      # expected_files: 'LICENSE.md,README.md,composer.json,CHANGELOG.md'
    
    secrets: inherit                        # Required to pass org-wide secrets like CODECOV_TOKEN.
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
