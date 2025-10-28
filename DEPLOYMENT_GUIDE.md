# Schema Deployment Guide

## How Pages Deployment Works

The `pages.yml` workflow now supports two scenarios:

### Scenario 1: Tag on Main Branch (Recommended)

**Process:**

1. Create your changes on a feature branch
2. Merge the PR to main
3. After merge, tag the commit on main: `git tag v1.0.2 && git push origin v1.0.2`
4. The workflow will trigger on tag push and deploy

### Scenario 2: Tag on Feature Branch (Now Supported)

**Process:**

1. Create your changes on a feature branch
2. Tag the commit on the branch: `git tag v1.0.2 && git push origin v1.0.2`
3. Merge the PR to main
4. The workflow will trigger on the merge to main, detect the tag, and deploy

## What Changed in the Workflow

### 1. Added Branch Trigger

```yaml
push:
    branches:
        - main # trigger on pushes to main
    tags:
        - "v*.*.*"
```

### 2. Enhanced Version Detection

The workflow now:

-   Detects when triggered by a tag push (uses tag name)
-   Detects when triggered by a branch push (finds latest version tag)
-   Uses version-specific schema files from `schema/versions/VERSION/`

### 3. Full Git History

Checkout now fetches full history to enable tag detection:

```yaml
with:
    fetch-depth: 0
```

## Recommended Workflow

**Best Practice:** Tag commits after they're on main.

```bash
# After your PR merges to main
git checkout main
git pull origin main

# Tag the latest commit
git tag v1.0.3
git push origin v1.0.3

# Workflow automatically deploys
```

## Troubleshooting

### Pages not deploying?

1. Check if the tag exists: `git tag -l "v*.*.*"`
2. Verify schema file exists: `schema/versions/VERSION/portableHouseData.schema.json`
3. Check workflow runs in Actions tab
4. Ensure tag format is `vX.Y.Z` (e.g., v1.0.2, v2.1.0)

### Wrong version deployed?

-   The workflow uses the **latest** version tag it finds
-   If multiple tags exist, it uses the highest semantic version
-   Ensure your intended version is the latest tag

## Version Numbering

Follow semantic versioning (SemVer):

-   **MAJOR** version when you make incompatible changes
-   **MINOR** version when you add functionality in a backward compatible manner
-   **PATCH** version when you make backward compatible bug fixes

Example: `v1.0.2` → `v1.1.0` → `v2.0.0`
