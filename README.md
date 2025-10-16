# Security Vulnerability Scanner Workflow

An automated GitHub Actions workflow that scans your code for security vulnerabilities and creates GitHub issues with AI-powered fix suggestions.

## 🔍 Vulnerability Identification Process

When the workflow runs, it automatically:

1. ✅ Scans your repository to identify the programming language
2. ✅ Selects the most appropriate security scanner based on the detected language
3. ✅ Identifies vulnerabilities in the repository using Snyk
4. ✅ Creates a GitHub issue with the identified vulnerabilities
5. ✅ Assigns GitHub Copilot to fix the issues and create a PR for the resolved vulnerabilities

## 🤖 GitHub Copilot Integration

When vulnerabilities are found, the workflow automatically:

1. ✅ Creates a detailed GitHub issue
2. ✅ Assigns it to GitHub Copilot SWE agent
3. ✅ Provides specific fix commands for each language
4. ✅ Includes comprehensive vulnerability context
5. ✅ Prioritizes based on severity

## 🔐 Setting Up Repository Secrets

Before integrating the security scanner, you need to add the following secrets to your repository:

### Required Secrets:

1. **SNYK_TOKEN** (Recommended)
   - Go to [snyk.io](https://snyk.io) and sign up or log in
   - Navigate to Account Settings
   - Copy your API token
   - In your GitHub repository: Settings → Secrets and variables → Actions → New repository secret
   - Name: `SNYK_TOKEN`
   - Paste your Snyk API token

2. **GH_TOKEN** (Required for issue creation)
   - Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - Select scope: `repo` (Full control of private repositories)
   - Generate and copy the token
   - In your repository: Settings → Secrets and variables → Actions → New repository secret
   - Name: `GH_TOKEN`
   - Paste your GitHub token

## 📦 Integrating with Your Repository

To use this security scanner in your own repository, follow these steps:

1. Create a new file in your repository: `.github/workflows/security-scan.yml`
2. Copy the YAML configuration below into that file
3. Replace `<YOUR-GITHUB-USERNAME>` with your GitHub username
4. Commit and push the file to your repository

The workflow will automatically start scanning your code based on the configured schedule or triggers.

```yaml
name: Security Scan Caller

on:
  schedule:
    - cron: '0 2 * * *'
  workflow_dispatch:
  pull_request:
    branches:
      - main
  push:
    branches:
      - main

permissions:
  contents: write
  issues: write
  pull-requests: write
  actions: read
  security-events: write

jobs:
  call-security-scan:
    uses: <YOUR-GITHUB-USERNAME>/security-workflows/.github/workflows/security-scan-reusable.yml@main
    with:
      language: 'auto'
      scanner: 'auto'
      severity-threshold: 'low'
      working-directory: '.'
      create-issue: true
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```