
# Secrets Scanner Action

This GitHub Action scans your repository for secrets using TruffleHog and uploads the results to a specified artifact API.

## Inputs

| Name                 | Description                                  | Required | Default  |
|----------------------|----------------------------------------------|----------|----------|
| `branch`             | Branch to scan.                              | No       | -        |
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
  trufflehog-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Run TruffleHog Action
        uses: your-org/trufflehog-scan-action@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          tenant_id: ${{ secrets.TENANT_ID }}
          artifact_api_token: ${{ secrets.TOKEN }}
          artifact_api_url: "https://cspm.dev.accuknox.com/api/v1/artifact/"
          label_id: "custom-label-123"

