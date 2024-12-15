
# Secrets Scanner Action

This GitHub Action scans your repository for secrets using TruffleHog and uploads the results to a specified artifact API.

## New 
Logic to dynamically determine the branch being scanned:

### Direct Push: Scans the pushed branch (e.g., dev, prod, etc.).
### Pull Requests: Scans only the PR source branch to check for secrets.
The action is fully generic now and allows users to dynamically scan any branch without hardcoding dev as default.

## Inputs

| Name                 | Description                                  | Required | Default  |
|----------------------|----------------------------------------------|----------|----------|
| `tenant_id`          | AccuKnox Tenant ID.                          | Yes      | -        |
| `artifact_api_token` | Authorization token for artifact API.        | Yes      | -        |
| `artifact_api_url`   | URL of the artifact API to upload results.   | Yes      | -        |
| `label_id`           | AccuKnox label                               | Yes      | -        |

## Example Workflow

```yaml
name: Secret Scan

on:
  push:
    branches:
      - dev
  pull_request:
    branches:
      - dev

jobs:
  secrets-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Run Secrets Scanner
        uses: salman-accuknox/secret-scan-action@main
        with:
          tenant_id: ${{ secrets.TENANT_ID }}
          artifact_api_token: ${{ secrets.ARTIFACT_API_TOKEN }}
          artifact_api_url: "https://cspm.dev.accuknox.com/api/v1/artifact/"
          label_id: "custom-label-123"

