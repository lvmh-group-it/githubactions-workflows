# githubactions-workflows

List of all workflow for lvmh can be include to other repos

## terraform

Location : .github/worflows/worflows-terraform.yaml

Description : 

| Info | value |
|--------------|------------------------------------------|
| **Location** | .github/worflows/worflows-terraform.yaml |
| **description** | Pipeline to check terraform code |

### inputs
- kics-ignore:

        default: false
        type: boolean
        description: "ignore kics failure"
- kics-level-failure:

        default: "high,medium"
        type: string
        description: "kics level failure"
- working_directory:

        default: "terraform"
        type: string
        description: "Terraform working directory"
- wiz_policy:

        default: "Default IaC policy"
        type: string
        description: "policy to use with wiz" 

## Secrets

- infracost_api_key:

        description: "Infracost api key"
        required: true

- LVMH_GITHUB_TOKEN:

        description: "Token for get token"
        required: true

- WIZ_CLIENT_ID:

        description: "Wiz Client ID sac"

- WIZ_CLIENT_SECRET:

        description: "Wiz Client Secret sac"

## Usage

Exemple to import in other pipeline :

```yaml
name: "GitHub Actions terraform"

on:
  pull_request:
  push:
    branches: [ "main" ]
  workflow_dispatch:
    inputs:
      logLevel:
        description: "Log level"
        required: true
        default: "warning"
      tags:
        description: "Test scenario tags"

jobs:
  call-workflow-lvmh-terraform:
    uses: lvmh-group-it/githubactions-workflows/.github/workflows/workflows-terraform.yaml@main
    with:
      working_directory: "."
    secrets:
      infracost_api_key: "${{ secrets.INFRACOST_API_KEY }}"
      LVMH_GITHUB_TOKEN: "${{ secrets.LVMH_GITHUB_TOKEN }}"
      WIZ_CLIENT_ID: "${{ secrets.WIZ_CLIENT_ID }}"
      WIZ_CLIENT_SECRET: "${{ secrets.WIZ_CLIENT_SECRET }}"
```