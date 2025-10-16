# Security Vulnerability Scanner with GitHub Copilot# Security Vulnerability Scanner# Security Vulnerability Scanner# 🔒 Centralized Security Workflows



Automated security scanning that detects vulnerabilities and creates GitHub issues with AI-powered fix suggestions from GitHub Copilot.



---Automated security vulnerability scanning for multiple programming languages with AI-powered fixes via GitHub Copilot.



## 🚀 How to Add Security Scan to Your Repository



### Step 1: Add Required Tokens## Supported LanguagesAutomated security vulnerability scanning for multiple programming languages with AI-powered fixes via GitHub Copilot.A production-ready, reusable GitHub Actions workflow system for automated security vulnerability scanning across multiple programming languages and frameworks.



Navigate to your repository → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**



Add these two secrets:Node.js • Python • Rust • Scala • Java • Go • .NET • Ruby • PHP



| Secret Name | Description | How to Get |

|-------------|-------------|------------|

| `SNYK_TOKEN` | Snyk API token for vulnerability scanning | 1. Go to [snyk.io](https://snyk.io)<br>2. Sign up/Login<br>3. Go to Account Settings<br>4. Copy your API token |## Quick Start## Supported Languages[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

| `GH_TOKEN` | GitHub token for creating issues | 1. Go to GitHub Settings → Developer settings<br>2. Personal access tokens → Tokens (classic)<br>3. Generate new token<br>4. Select scope: `repo` (Full control)<br>5. Copy the token |



> **Note:** `SNYK_TOKEN` is optional if you want to use language-specific scanners only. `GH_TOKEN` is required for issue creation.

### Step 1: Setup Secrets[![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-2088FF?logo=github-actions&logoColor=white)](https://github.com/features/actions)

---



### Step 2: Create Security Workflow File

Add these secrets to your repository (Settings → Secrets → Actions):Node.js • Python • Rust • Scala • Java • Go • .NET • Ruby • PHP

In your repository, create this file: `.github/workflows/security-scan.yml`



```yaml

name: Security Scan- `SNYK_TOKEN` - Get from [snyk.io](https://snyk.io) (optional but recommended)## 🎯 Overview



on:- `GH_TOKEN` - GitHub Personal Access Token with `repo` scope (required for issue creation)

  schedule:

    - cron: '0 2 * * *'  # Runs daily at 2 AM UTC## Quick Start

  workflow_dispatch:      # Allows manual trigger

  pull_request:### Step 2: Create Workflow File

    branches: [main]

This repository provides a **centralized security scanning solution** that can be imported and used by any repository in your organization. It supports multiple programming languages, auto-detects project types, and integrates with GitHub Copilot for automated vulnerability fixes.

permissions:

  contents: readCreate `.github/workflows/security-scan.yml` in your repository:

  issues: write

  pull-requests: write### Step 1: Setup Secrets

  security-events: write

```yaml

jobs:

  security-scan:name: Security Scan## ✨ Key Features

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

    with:

      language: 'auto'              # Auto-detects your project language

      scanner: 'auto'               # Auto-selects best scanneron:Add these secrets to your repository (Settings → Secrets → Actions):

      severity-threshold: 'low'     # Reports all severity levels

      create-issue: true            # Creates GitHub issue with results  schedule:

    secrets:

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}    - cron: '0 2 * * *'  # Daily at 2 AM- 🔄 **Truly Reusable**: Import once, use everywhere

      GH_TOKEN: ${{ secrets.GH_TOKEN }}

```  workflow_dispatch:      # Manual trigger



---  pull_request:- `SNYK_TOKEN` - Get from [snyk.io](https://snyk.io) (optional but recommended)- 🌐 **Multi-Language Support**: Node.js, Python, Rust, Scala, Java, Go, .NET, Ruby, PHP



### Step 3: Run the Workflow    branches: [main]



**Option A - Automatic Scan:**- `GH_TOKEN` - GitHub Personal Access Token with `repo` scope (required for issue creation)- 🤖 **AI-Powered Fixes**: Automatic assignment to GitHub Copilot

- The workflow runs automatically every day at 2 AM UTC

- Also runs on every pull request to main branchpermissions:



**Option B - Manual Scan:**  contents: read- 🧩 **Modular Architecture**: Use the full workflow or individual actions

1. Go to your repository on GitHub

2. Click **Actions** tab  issues: write

3. Select **Security Scan** workflow from the left sidebar

4. Click **Run workflow** button (top right)  pull-requests: write### Step 2: Create Workflow File- 📊 **Rich Reporting**: Detailed vulnerability reports and GitHub Issues

5. Click the green **Run workflow** button

  security-events: write

---

- ⚙️ **Highly Configurable**: Customize for your specific needs

### Step 4: Review Results

jobs:

After the scan completes:

  security-scan:Create `.github/workflows/security-scan.yml` in your repository:

1. **Check GitHub Actions Summary:**

   - Go to Actions → Click on the workflow run    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

   - View summary with vulnerability counts by severity

    with:## 🚀 Quick Start

2. **Download Artifacts:**

   - Scroll to bottom of workflow run      language: 'auto'

   - Download `vulnerability-data` artifact

   - Contains JSON files and markdown report      scanner: 'auto'```yaml



3. **Review GitHub Issue:**      severity-threshold: 'low'

   - If vulnerabilities found, an issue is automatically created

   - Issue contains:      create-issue: truename: Security Scan### For Other Repositories (Recommended Usage)

     - Detailed vulnerability information

     - Fix commands for your language    secrets:

     - CVSS scores and CVE IDs

     - **Assigned to GitHub Copilot** for AI-powered fixes      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}



---      GH_TOKEN: ${{ secrets.GH_TOKEN }}



## 🤖 GitHub Copilot Integration```on:In any repository where you want to add security scanning, create `.github/workflows/security-scan.yml`:



### What Happens Automatically:



1. **Issue Created:** When vulnerabilities are detected, a GitHub issue is automatically created### Step 3: Run the Workflow  schedule:

2. **Copilot Assigned:** The issue is assigned to GitHub Copilot SWE agent

3. **AI Analysis:** Copilot analyzes the vulnerabilities and provides:

   - Specific fix commands for your programming language

   - Risk assessment for each vulnerability**Option A - Automatic:** Wait for scheduled run (daily at 2 AM)    - cron: '0 2 * * *'  # Daily at 2 AM```yaml

   - Compatibility analysis

   - Testing recommendations

   - Alternative solutions if needed

**Option B - Manual:**   workflow_dispatch:      # Manual triggername: Security Scan

### Using Copilot Fixes:

1. Go to Actions tab

1. **Open the Issue:** Navigate to the created security issue in your repository

2. **Review Copilot's Suggestions:** Read the AI-generated fix recommendations2. Select "Security Scan" workflow  pull_request:

3. **Apply Fixes:** Copy the suggested commands and run in your project:

   ```bash3. Click "Run workflow"

   # Example for Node.js

   npm install package-name@fixed-version    branches: [main]on:

   

   # Example for Python## Configuration Options

   pip install package-name==fixed-version

   ```  schedule:

4. **Test Changes:** Run your tests to ensure fixes don't break functionality

5. **Create Pull Request:** Commit and push your fixes### Inputs

6. **Close Issue:** Once fixed, close the security issue

permissions:    - cron: '0 2 * * *'  # Daily at 2 AM

---

| Input | Description | Default |

## 🌐 Supported Languages

|-------|-------------|---------|  contents: read  workflow_dispatch:

| Language | Auto-Detected By | Default Scanner | Alternative Scanner |

|----------|------------------|-----------------|-------------------|| `language` | Programming language (`auto`, `nodejs`, `python`, `rust`, `scala`, `java`, `go`, `dotnet`, `ruby`, `php`) | `auto` |

| **Node.js** | `package.json` | Snyk or npm-audit | - |

| **Python** | `requirements.txt`, `setup.py`, `pyproject.toml`, `Pipfile` | Snyk or pip-audit | - || `scanner` | Scanner tool (`auto`, `snyk`, `npm-audit`, `pip-audit`, `cargo-audit`, `trivy`, etc.) | `auto` |  issues: write  pull_request:

| **Rust** | `Cargo.toml` | cargo-audit | - |

| **Scala** | `build.sbt`, `build.sc` | Snyk or Trivy | - || `severity-threshold` | Minimum severity (`low`, `medium`, `high`, `critical`) | `low` |

| **Java** | `pom.xml`, `build.gradle`, `build.gradle.kts` | Snyk or OWASP Dependency Check | - |

| **Go** | `go.mod` | govulncheck | - || `working-directory` | Directory to scan | `.` |  pull-requests: write    branches: [main]

| **.NET** | `*.csproj`, `*.sln` | dotnet list | - |

| **Ruby** | `Gemfile` | bundler-audit | - || `create-issue` | Create GitHub issue | `true` |

| **PHP** | `composer.json` | composer-audit | - |

  security-events: write

### How Language Detection Works:

### Language-Specific Scanners

1. Workflow checks your repository for language-specific files

2. Automatically selects the appropriate scannerpermissions:

3. Installs necessary dependencies

4. Runs vulnerability scan| Language | Default Scanner | Alternative |

5. Normalizes results to common format

|----------|----------------|-------------|jobs:  contents: read

---

| Node.js | Snyk / npm-audit | - |

## 🔧 Configuration Options

| Python | Snyk / pip-audit | - |  security-scan:  issues: write

Customize the workflow by modifying the `with:` section:

| Rust | cargo-audit | - |

```yaml

with:| Scala | Snyk / Trivy | - |    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main  pull-requests: write

  language: 'auto'              # Options: auto, nodejs, python, rust, scala, java, go, dotnet, ruby, php

  scanner: 'auto'               # Options: auto, snyk, npm-audit, pip-audit, cargo-audit, trivy, etc.| Java | Snyk / OWASP | - |

  severity-threshold: 'low'     # Options: low, medium, high, critical

  working-directory: '.'        # Change if your code is in a subdirectory| Go | govulncheck | - |    with:  security-events: write

  create-issue: true            # Set to false to disable issue creation

```| .NET | dotnet list | - |



### Advanced Examples:| Ruby | bundler-audit | - |      language: 'auto'              # Auto-detect language



**Scan only high/critical vulnerabilities:**| PHP | composer-audit | - |

```yaml

with:      scanner: 'auto'               # Auto-select scannerjobs:

  severity-threshold: 'high'

```## Examples



**Scan specific language:**      severity-threshold: 'low'     # Report all severities  security-scan:

```yaml

with:### Scan Specific Language

  language: 'python'

  scanner: 'pip-audit'      create-issue: true            # Create GitHub issue    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

```

```yaml

**Scan multiple directories (monorepo):**

```yamljobs:    secrets:    with:

jobs:

  scan-frontend:  scan-python:

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

    with:    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}      language: 'auto'  # Auto-detect or specify: nodejs, python, rust, scala, java, go, etc.

      working-directory: './frontend'

      language: 'nodejs'    with:

    secrets:

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}      language: 'python'      GH_TOKEN: ${{ secrets.GH_TOKEN }}      scanner: 'auto'   # Auto-select scanner or specify: snyk, npm-audit, pip-audit, etc.

      GH_TOKEN: ${{ secrets.GH_TOKEN }}

        scanner: 'pip-audit'

  scan-backend:

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main    secrets:```      create-issue: true

    with:

      working-directory: './backend'      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

      language: 'python'

    secrets:      GH_TOKEN: ${{ secrets.GH_TOKEN }}      severity-threshold: 'low'

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

      GH_TOKEN: ${{ secrets.GH_TOKEN }}```

```

### Step 3: Run the Workflow    secrets:

---

### Scan Multiple Directories

## 🛠️ Troubleshooting

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

### Issue: "SNYK_TOKEN not found" error

```yaml

**Solution:**

1. Go to your repository Settingsjobs:**Option A - Automatic:** Wait for scheduled run (daily at 2 AM)      GH_TOKEN: ${{ secrets.GH_TOKEN }}

2. Click Secrets and variables → Actions

3. Click "New repository secret"  scan-frontend:

4. Name: `SNYK_TOKEN`

5. Value: Paste your Snyk API token    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main```

6. Click "Add secret"

    with:

---

      working-directory: './frontend'**Option B - Manual:** 

### Issue: "Cannot create GitHub issue" or "GH_TOKEN invalid"

      language: 'nodejs'

**Solution:**

1. Create a new Personal Access Token:    secrets:1. Go to Actions tabThat's it! Your repository now has automated security scanning.

   - Go to GitHub Settings → Developer settings

   - Personal access tokens → Tokens (classic)      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

   - Click "Generate new token (classic)"

   - Select scopes: `repo` (all checkboxes under repo)      GH_TOKEN: ${{ secrets.GH_TOKEN }}2. Select "Security Scan" workflow

   - Generate and copy the token

2. Add to repository secrets:  

   - Repository Settings → Secrets and variables → Actions

   - New repository secret  scan-backend:3. Click "Run workflow"## 📁 What's Included

   - Name: `GH_TOKEN`

   - Value: Paste the token    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main



---    with:



### Issue: "No vulnerabilities detected" but you expect some      working-directory: './backend'



**Possible Causes & Solutions:**      language: 'python'## How It Works```



1. **Wrong working directory:**    secrets:

   - Check if your code is in a subdirectory

   - Set `working-directory: './your-directory'`      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}security-workflows/



2. **Language not detected:**      GH_TOKEN: ${{ secrets.GH_TOKEN }}

   - Manually specify language: `language: 'nodejs'` (or python, java, etc.)

   - Check if language-specific files exist (package.json, requirements.txt, etc.)``````├── .github/



3. **No dependencies installed:**

   - Make sure your dependency file exists (package.json, requirements.txt, etc.)

   - Ensure dependencies are properly declared### High Severity Only┌─────────────────────────────────────────────────────────────┐│   ├── workflows/



4. **Your project is actually secure:**

   - Check if your dependencies are up-to-date

   - No known vulnerabilities might mean you're good! ✅```yaml│ 1. Detect Language (Node.js, Python, Rust, Scala, etc.)    ││   │   ├── security-scan-reusable.yml    # Main reusable workflow



---jobs:



### Issue: "Workflow not found" or "Action not found"  scan:└─────────────────────────────────────────────────────────────┘│   │   └── security-scan-caller.yml      # Example caller (for this repo)



**Solution:**    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

- Ensure you're using the correct path:

  ```yaml    with:                            ↓│   │

  uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

  ```      severity-threshold: 'high'

- Check that you're using `@main` (not `@master`)

    secrets:┌─────────────────────────────────────────────────────────────┐│   └── actions/                           # Composite actions

---

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

### Issue: "Permission denied" or "Insufficient permissions"

      GH_TOKEN: ${{ secrets.GH_TOKEN }}│ 2. Select Scanner (Snyk, npm-audit, pip-audit, etc.)       ││       ├── scan-vulnerabilities/          # Multi-language scanning

**Solution:**

1. Check workflow permissions in your workflow file:```

   ```yaml

   permissions:└─────────────────────────────────────────────────────────────┘│       ├── process-vulnerabilities/       # Results processing

     contents: read

     issues: write## What You Get

     pull-requests: write

     security-events: write                            ↓│       └── create-security-issue/         # GitHub issue creation

   ```

### 1. GitHub Actions Summary

2. Check repository settings:

   - Settings → Actions → General- Vulnerability counts by severity┌─────────────────────────────────────────────────────────────┐│

   - Workflow permissions → "Read and write permissions"

   - Save- Scan details and timestamps



---│ 3. Install Dependencies & Run Scan                          │├── README.md                              # This file



### Issue: Copilot not assigned to issue### 2. Downloadable Artifacts



**Possible Causes:**- `full-scan-results.json` - Complete scan data└─────────────────────────────────────────────────────────────┘├── CONTRIBUTING.md                        # Contribution guidelines



1. **GitHub Copilot not available in your organization:**- `detailed-vulnerabilities.json` - Processed vulnerabilities

   - This feature requires GitHub Copilot subscription

   - Issue will still be created with fix suggestions- `vulnerability-context.md` - Human-readable report                            ↓└── LICENSE                                # MIT License



2. **Permissions issue:**

   - Ensure `GH_TOKEN` has full `repo` scope

### 3. GitHub Issue (Auto-Created)┌─────────────────────────────────────────────────────────────┐```

---

- Detailed vulnerability information

### Issue: Scan takes too long or times out

- Language-specific fix commands│ 4. Process & Normalize Results                              │

**Solutions:**

- CVSS scores and CVE IDs

1. **Scan specific directories only:**

   ```yaml- Assigned to GitHub Copilot└─────────────────────────────────────────────────────────────┘## 🎨 Supported Languages & Scanners

   with:

     working-directory: './src'- Labeled by severity

   ```

                            ↓

2. **Skip code scanning (dependency scan only):**

   - Use language-specific scanners instead of Snyk## Troubleshooting

   - Example: `scanner: 'npm-audit'` for Node.js

┌─────────────────────────────────────────────────────────────┐| Language | Auto-Detected Files | Default Scanner | Alternative Scanners |

3. **Increase timeout (in your workflow):**

   ```yaml**"SNYK_TOKEN not found"**

   jobs:

     security-scan:→ Add secret in repository Settings → Secrets → Actions│ 5. Create GitHub Issue with Fix Commands                    │|----------|-------------------|-----------------|---------------------|

       timeout-minutes: 60

       uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

   ```

**"Cannot create issue"**└─────────────────────────────────────────────────────────────┘| **Node.js** | `package.json` | Snyk / npm-audit | - |

---

→ Ensure `GH_TOKEN` has `repo` scope

### Issue: False positives in scan results

                            ↓| **Python** | `requirements.txt`, `setup.py`, `pyproject.toml` | Snyk / pip-audit | - |

**Solutions:**

**"No vulnerabilities detected"**

1. **Increase severity threshold:**

   ```yaml→ Verify correct language detection and working directory┌─────────────────────────────────────────────────────────────┐| **Rust** | `Cargo.toml` | cargo-audit | - |

   with:

     severity-threshold: 'high'  # Only critical and high

   ```

**"Action not found"**│ 6. Assign to GitHub Copilot for AI-Powered Fixes           │| **Scala** | `build.sbt`, `build.sc` | Snyk / Trivy | - |

2. **Review and ignore specific vulnerabilities:**

   - Check if vulnerability applies to your use case→ Use full path: `denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main`

   - Document why it's not applicable

   - Use Snyk ignore policies if needed└─────────────────────────────────────────────────────────────┘| **Java** | `pom.xml`, `build.gradle` | Snyk / OWASP Dependency Check | - |



---## License



## 📊 What You Get```| **Go** | `go.mod` | govulncheck | - |



After each scan, you receive:MIT License - See [LICENSE](LICENSE) file for details.



1. **GitHub Actions Summary:**| **.NET** | `*.csproj`, `*.sln` | dotnet list | - |

   - Total vulnerabilities count

   - Breakdown by severity (Critical, High, Medium, Low)---

   - Scan timestamp and language detected

## Configuration Options| **Ruby** | `Gemfile` | bundler-audit | - |

2. **Artifacts (Downloadable):**

   - `full-scan-results.json` - Complete raw scan data**Made for secure software development** 🔒

   - `detailed-vulnerabilities.json` - Processed vulnerability list

   - `vulnerability-context.md` - Human-readable report| **PHP** | `composer.json` | composer-audit | - |



3. **GitHub Issue (if vulnerabilities found):**### Inputs

   - Title: "Security Vulnerability Scan - [Date] - [X] vulnerabilities found"

   - Labels: `security`, `vulnerability`, `ai-fix-requested`, `copilot-task`## 📚 Usage Examples

   - Content: Detailed info for each vulnerability

   - Assignment: GitHub Copilot SWE agent (if available)| Input | Description | Default |



---|-------|-------------|---------|### Basic Usage (Auto-Detection)



## 📞 Need Help?| `language` | Programming language (`auto`, `nodejs`, `python`, `rust`, `scala`, `java`, `go`, `dotnet`, `ruby`, `php`) | `auto` |



If you encounter issues not covered here:| `scanner` | Scanner tool (`auto`, `snyk`, `npm-audit`, `pip-audit`, `cargo-audit`, `trivy`, etc.) | `auto` |```yaml



1. Check [GitHub Actions logs](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/using-workflow-run-logs) for detailed error messages| `severity-threshold` | Minimum severity (`low`, `medium`, `high`, `critical`) | `low` |jobs:

2. Verify all secrets are correctly set

3. Ensure your repository has the required language files| `working-directory` | Directory to scan | `.` |  scan:

4. Check that workflow permissions are properly configured

| `create-issue` | Create GitHub issue | `true` |    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

---

    secrets:

**🔒 Keep your code secure!**

### Language-Specific Scanners      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

      GH_TOKEN: ${{ secrets.GH_TOKEN }}

| Language | Default Scanner | Alternative |```

|----------|----------------|-------------|

| Node.js | Snyk / npm-audit | - |### Scan Specific Language

| Python | Snyk / pip-audit | - |

| Rust | cargo-audit | - |```yaml

| Scala | Snyk / Trivy | - |jobs:

| Java | Snyk / OWASP | - |  scan-python:

| Go | govulncheck | - |    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

| .NET | dotnet list | - |    with:

| Ruby | bundler-audit | - |      language: 'python'

| PHP | composer-audit | - |      scanner: 'pip-audit'

    secrets:

## Examples      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

```

### Scan Specific Language

### Scan Multiple Directories

```yaml

jobs:```yaml

  scan-python:jobs:

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main  scan-frontend:

    with:    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

      language: 'python'    with:

      scanner: 'pip-audit'      working-directory: './frontend'

    secrets:      language: 'nodejs'

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}    secrets:

      GH_TOKEN: ${{ secrets.GH_TOKEN }}      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

```      GH_TOKEN: ${{ secrets.GH_TOKEN }}

  

### Scan Multiple Directories  scan-backend:

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

```yaml    with:

jobs:      working-directory: './backend'

  scan-frontend:      language: 'python'

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main    secrets:

    with:      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

      working-directory: './frontend'      GH_TOKEN: ${{ secrets.GH_TOKEN }}

      language: 'nodejs'```

    secrets:

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}### Use Individual Actions (Advanced)

      GH_TOKEN: ${{ secrets.GH_TOKEN }}

  ```yaml

  scan-backend:jobs:

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main  custom-scan:

    with:    runs-on: ubuntu-latest

      working-directory: './backend'    steps:

      language: 'python'      - uses: actions/checkout@v4

    secrets:      

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}      - name: Scan vulnerabilities

      GH_TOKEN: ${{ secrets.GH_TOKEN }}        id: scan

```        uses: denukedissanayake/security-workflows/.github/actions/scan-vulnerabilities@main

        with:

### High Severity Only          snyk-token: ${{ secrets.SNYK_TOKEN }}

          language: 'auto'

```yaml      

jobs:      - name: Process results

  scan:        id: process

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main        uses: denukedissanayake/security-workflows/.github/actions/process-vulnerabilities@main

    with:        with:

      severity-threshold: 'high'          scan-results-path: ${{ steps.scan.outputs.scan-results-path }}

    secrets:          repository: ${{ github.repository }}

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}      

      GH_TOKEN: ${{ secrets.GH_TOKEN }}      # Add your custom logic here

```      - name: Send to Slack

        if: steps.process.outputs.has-vulnerabilities == 'true'

## What You Get        run: |

          echo "Found ${{ steps.process.outputs.vulnerability-count }} vulnerabilities!"

### 1. GitHub Actions Summary          # Your custom notification logic

- Vulnerability counts by severity```

- Scan details and timestamps

## ⚙️ Configuration Options

### 2. Downloadable Artifacts

- `full-scan-results.json` - Complete scan data### Workflow Inputs

- `detailed-vulnerabilities.json` - Processed vulnerabilities

- `vulnerability-context.md` - Human-readable report| Input | Description | Required | Default |

|-------|-------------|----------|---------|

### 3. GitHub Issue (Auto-Created)| `working-directory` | Directory to scan | No | `.` |

- Detailed vulnerability information| `language` | Programming language | No | `auto` |

- Language-specific fix commands| `scanner` | Scanner tool to use | No | `auto` |

- CVSS scores and CVE IDs| `severity-threshold` | Minimum severity to report | No | `low` |

- Assigned to GitHub Copilot| `create-issue` | Create GitHub issue | No | `true` |

- Labeled by severity

### Workflow Secrets

## Troubleshooting

| Secret | Description | Required |

**"SNYK_TOKEN not found"**|--------|-------------|----------|

→ Add secret in repository Settings → Secrets → Actions| `SNYK_TOKEN` | Snyk API token | Conditional* |

| `GH_TOKEN` | GitHub token for issue creation | Conditional** |

**"Cannot create issue"**

→ Ensure `GH_TOKEN` has `repo` scope\* Required if using Snyk scanner  

\** Required if `create-issue: true`

**"No vulnerabilities detected"**

→ Verify correct language detection and working directory### Workflow Outputs



**"Action not found"**| Output | Description |

→ Use full path: `denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main`|--------|-------------|

| `vulnerabilities-found` | Number of vulnerabilities detected |

## License| `has-vulnerabilities` | Boolean indicating if vulnerabilities exist |



MIT License - See [LICENSE](LICENSE) file for details.## 🔧 Prerequisites



---### 1. Snyk Token (Optional but Recommended)



**Made for secure software development** 🔒1. Sign up at [snyk.io](https://snyk.io)

2. Get your API token from Account Settings
3. Add as repository secret: `SNYK_TOKEN`

### 2. GitHub Token (For Issue Creation)

**Option A: Use GITHUB_TOKEN (Limited)**
```yaml
secrets:
  GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**Option B: Personal Access Token (Recommended)**
1. Create a PAT with `repo` scope
2. Add as repository secret: `GH_TOKEN`

### 3. Repository Permissions

Ensure your workflow has the necessary permissions:

```yaml
permissions:
  contents: read
  issues: write
  pull-requests: write
  security-events: write
```

## 🤖 GitHub Copilot Integration

When vulnerabilities are found, the workflow automatically:

1. ✅ Creates a detailed GitHub issue
2. ✅ Assigns it to GitHub Copilot SWE agent
3. ✅ Provides specific fix commands for each language
4. ✅ Includes comprehensive vulnerability context
5. ✅ Prioritizes based on severity

Example issue title:
```
Security Vulnerability Scan - 2025-10-16 - 12 vulnerabilities found
```

Labels automatically applied:
- `security`
- `vulnerability`
- `ai-fix-requested`
- `copilot-task`
- `high-priority` (if critical/high severity found)

## 📊 What Gets Generated

### 1. GitHub Actions Summary
- Vulnerability counts by severity
- Scan date and project info
- Links to detailed reports

### 2. Artifacts (Available for Download)
- `full-scan-results.json` - Complete scan data
- `detailed-vulnerabilities.json` - Processed vulnerability list
- `vulnerability-context.md` - Human-readable report

### 3. GitHub Issue (if enabled)
- Comprehensive vulnerability details
- Language-specific fix commands
- Copilot assistance requests
- Severity-based prioritization

## 🔒 Security Best Practices

- ✅ **Never hardcode tokens** - Always use secrets
- ✅ **Use least-privilege permissions** - Only grant what's needed
- ✅ **Run scans regularly** - Schedule daily or on each PR
- ✅ **Review and fix promptly** - Don't let vulnerabilities accumulate
- ✅ **Keep dependencies updated** - Use automated tools like Dependabot
- ✅ **Monitor scan results** - Review the generated reports

## 🛠️ Customization Examples

### Only Scan on Pull Requests

```yaml
on:
  pull_request:
    branches: [main, develop]

jobs:
  scan:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

### Disable Issue Creation (Reports Only)

```yaml
jobs:
  scan:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    with:
      create-issue: false  # Just scan and report
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

### High Severity Only

```yaml
jobs:
  scan:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    with:
      severity-threshold: 'high'  # Only report high and critical
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

## 📖 Documentation

- [Technical Documentation](.github/README.md) - Complete workflow and actions reference
- [Contributing Guidelines](CONTRIBUTING.md) - How to contribute
- [License](LICENSE) - MIT License

## 🐛 Troubleshooting

### "SNYK_TOKEN not found"
**Solution**: Add the secret in repository Settings → Secrets and variables → Actions → New repository secret

### "Cannot create issue"
**Solution**: 
- Ensure `GH_TOKEN` has `repo` scope
- Or use `GITHUB_TOKEN` (may have limited functionality)
- Check repository permissions for issues

### "No vulnerabilities detected but expected some"
**Solution**:
- Verify your language is correctly detected
- Check `working-directory` is correct
- Ensure dependencies are installed
- Review scanner selection

### "Action not found"
**Solution**:
- Use the full repository path: `denukedissanayake/security-workflows/.github/workflows/...@main`
- Verify the branch name (use `@main` or `@v1.0.0`)
- Check that the workflow file exists in the specified path

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test thoroughly with different languages
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Snyk** - Multi-language vulnerability scanning
- **GitHub Actions** - Workflow automation
- **GitHub Copilot** - AI-powered security fixes
- Community contributors and testers

## 📞 Support

- 📖 **Documentation**: [Technical Docs](.github/README.md)
- 🐛 **Issues**: [GitHub Issues](https://github.com/denukedissanayake/security-workflows/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/denukedissanayake/security-workflows/discussions)

---

**Made with ❤️ for secure software development**

*Star ⭐ this repository if you find it useful!*
