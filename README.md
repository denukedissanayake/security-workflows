# 🔒 Centralized Security Workflows

A production-ready, reusable GitHub Actions workflow system for automated security vulnerability scanning across multiple programming languages and frameworks.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-2088FF?logo=github-actions&logoColor=white)](https://github.com/features/actions)

## 🎯 Overview

This repository provides a **centralized security scanning solution** that can be imported and used by any repository in your organization. It supports multiple programming languages, auto-detects project types, and integrates with GitHub Copilot for automated vulnerability fixes.

## ✨ Key Features

- 🔄 **Truly Reusable**: Import once, use everywhere
- 🌐 **Multi-Language Support**: Node.js, Python, Rust, Scala, Java, Go, .NET, Ruby, PHP
- 🤖 **AI-Powered Fixes**: Automatic assignment to GitHub Copilot
- 🧩 **Modular Architecture**: Use the full workflow or individual actions
- 📊 **Rich Reporting**: Detailed vulnerability reports and GitHub Issues
- ⚙️ **Highly Configurable**: Customize for your specific needs

## 🚀 Quick Start

### For Other Repositories (Recommended Usage)

In any repository where you want to add security scanning, create `.github/workflows/security-scan.yml`:

```yaml
name: Security Scan

on:
  schedule:
    - cron: '0 2 * * *'  # Daily at 2 AM
  workflow_dispatch:
  pull_request:
    branches: [main]

permissions:
  contents: read
  issues: write
  pull-requests: write
  security-events: write

jobs:
  security-scan:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    with:
      language: 'auto'  # Auto-detect or specify: nodejs, python, rust, scala, java, go, etc.
      scanner: 'auto'   # Auto-select scanner or specify: snyk, npm-audit, pip-audit, etc.
      create-issue: true
      severity-threshold: 'low'
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

That's it! Your repository now has automated security scanning.

## 📁 What's Included

```
security-workflows/
├── .github/
│   ├── workflows/
│   │   ├── security-scan-reusable.yml    # Main reusable workflow
│   │   └── security-scan-caller.yml      # Example caller (for this repo)
│   │
│   └── actions/                           # Composite actions
│       ├── scan-vulnerabilities/          # Multi-language scanning
│       ├── process-vulnerabilities/       # Results processing
│       └── create-security-issue/         # GitHub issue creation
│
├── README.md                              # This file
├── CONTRIBUTING.md                        # Contribution guidelines
└── LICENSE                                # MIT License
```

## 🎨 Supported Languages & Scanners

| Language | Auto-Detected Files | Default Scanner | Alternative Scanners |
|----------|-------------------|-----------------|---------------------|
| **Node.js** | `package.json` | Snyk / npm-audit | - |
| **Python** | `requirements.txt`, `setup.py`, `pyproject.toml` | Snyk / pip-audit | - |
| **Rust** | `Cargo.toml` | cargo-audit | - |
| **Scala** | `build.sbt`, `build.sc` | Snyk / Trivy | - |
| **Java** | `pom.xml`, `build.gradle` | Snyk / OWASP Dependency Check | - |
| **Go** | `go.mod` | govulncheck | - |
| **.NET** | `*.csproj`, `*.sln` | dotnet list | - |
| **Ruby** | `Gemfile` | bundler-audit | - |
| **PHP** | `composer.json` | composer-audit | - |

## 📚 Usage Examples

### Basic Usage (Auto-Detection)

```yaml
jobs:
  scan:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

### Scan Specific Language

```yaml
jobs:
  scan-python:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    with:
      language: 'python'
      scanner: 'pip-audit'
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

### Scan Multiple Directories

```yaml
jobs:
  scan-frontend:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    with:
      working-directory: './frontend'
      language: 'nodejs'
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
  
  scan-backend:
    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
    with:
      working-directory: './backend'
      language: 'python'
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

### Use Individual Actions (Advanced)

```yaml
jobs:
  custom-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Scan vulnerabilities
        id: scan
        uses: denukedissanayake/security-workflows/.github/actions/scan-vulnerabilities@main
        with:
          snyk-token: ${{ secrets.SNYK_TOKEN }}
          language: 'auto'
      
      - name: Process results
        id: process
        uses: denukedissanayake/security-workflows/.github/actions/process-vulnerabilities@main
        with:
          scan-results-path: ${{ steps.scan.outputs.scan-results-path }}
          repository: ${{ github.repository }}
      
      # Add your custom logic here
      - name: Send to Slack
        if: steps.process.outputs.has-vulnerabilities == 'true'
        run: |
          echo "Found ${{ steps.process.outputs.vulnerability-count }} vulnerabilities!"
          # Your custom notification logic
```

## ⚙️ Configuration Options

### Workflow Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `working-directory` | Directory to scan | No | `.` |
| `language` | Programming language | No | `auto` |
| `scanner` | Scanner tool to use | No | `auto` |
| `severity-threshold` | Minimum severity to report | No | `low` |
| `create-issue` | Create GitHub issue | No | `true` |

### Workflow Secrets

| Secret | Description | Required |
|--------|-------------|----------|
| `SNYK_TOKEN` | Snyk API token | Conditional* |
| `GH_TOKEN` | GitHub token for issue creation | Conditional** |

\* Required if using Snyk scanner  
\** Required if `create-issue: true`

### Workflow Outputs

| Output | Description |
|--------|-------------|
| `vulnerabilities-found` | Number of vulnerabilities detected |
| `has-vulnerabilities` | Boolean indicating if vulnerabilities exist |

## 🔧 Prerequisites

### 1. Snyk Token (Optional but Recommended)

1. Sign up at [snyk.io](https://snyk.io)
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
