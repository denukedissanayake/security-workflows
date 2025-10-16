# Security Vulnerability Scanner# 🔒 Centralized Security Workflows



Automated security vulnerability scanning for multiple programming languages with AI-powered fixes via GitHub Copilot.A production-ready, reusable GitHub Actions workflow system for automated security vulnerability scanning across multiple programming languages and frameworks.



## Supported Languages[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-2088FF?logo=github-actions&logoColor=white)](https://github.com/features/actions)

Node.js • Python • Rust • Scala • Java • Go • .NET • Ruby • PHP

## 🎯 Overview

## Quick Start

This repository provides a **centralized security scanning solution** that can be imported and used by any repository in your organization. It supports multiple programming languages, auto-detects project types, and integrates with GitHub Copilot for automated vulnerability fixes.

### Step 1: Setup Secrets

## ✨ Key Features

Add these secrets to your repository (Settings → Secrets → Actions):

- 🔄 **Truly Reusable**: Import once, use everywhere

- `SNYK_TOKEN` - Get from [snyk.io](https://snyk.io) (optional but recommended)- 🌐 **Multi-Language Support**: Node.js, Python, Rust, Scala, Java, Go, .NET, Ruby, PHP

- `GH_TOKEN` - GitHub Personal Access Token with `repo` scope (required for issue creation)- 🤖 **AI-Powered Fixes**: Automatic assignment to GitHub Copilot

- 🧩 **Modular Architecture**: Use the full workflow or individual actions

### Step 2: Create Workflow File- 📊 **Rich Reporting**: Detailed vulnerability reports and GitHub Issues

- ⚙️ **Highly Configurable**: Customize for your specific needs

Create `.github/workflows/security-scan.yml` in your repository:

## 🚀 Quick Start

```yaml

name: Security Scan### For Other Repositories (Recommended Usage)



on:In any repository where you want to add security scanning, create `.github/workflows/security-scan.yml`:

  schedule:

    - cron: '0 2 * * *'  # Daily at 2 AM```yaml

  workflow_dispatch:      # Manual triggername: Security Scan

  pull_request:

    branches: [main]on:

  schedule:

permissions:    - cron: '0 2 * * *'  # Daily at 2 AM

  contents: read  workflow_dispatch:

  issues: write  pull_request:

  pull-requests: write    branches: [main]

  security-events: write

permissions:

jobs:  contents: read

  security-scan:  issues: write

    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main  pull-requests: write

    with:  security-events: write

      language: 'auto'              # Auto-detect language

      scanner: 'auto'               # Auto-select scannerjobs:

      severity-threshold: 'low'     # Report all severities  security-scan:

      create-issue: true            # Create GitHub issue    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

    secrets:    with:

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}      language: 'auto'  # Auto-detect or specify: nodejs, python, rust, scala, java, go, etc.

      GH_TOKEN: ${{ secrets.GH_TOKEN }}      scanner: 'auto'   # Auto-select scanner or specify: snyk, npm-audit, pip-audit, etc.

```      create-issue: true

      severity-threshold: 'low'

### Step 3: Run the Workflow    secrets:

      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

**Option A - Automatic:** Wait for scheduled run (daily at 2 AM)      GH_TOKEN: ${{ secrets.GH_TOKEN }}

```

**Option B - Manual:** 

1. Go to Actions tabThat's it! Your repository now has automated security scanning.

2. Select "Security Scan" workflow

3. Click "Run workflow"## 📁 What's Included



## How It Works```

security-workflows/

```├── .github/

┌─────────────────────────────────────────────────────────────┐│   ├── workflows/

│ 1. Detect Language (Node.js, Python, Rust, Scala, etc.)    ││   │   ├── security-scan-reusable.yml    # Main reusable workflow

└─────────────────────────────────────────────────────────────┘│   │   └── security-scan-caller.yml      # Example caller (for this repo)

                            ↓│   │

┌─────────────────────────────────────────────────────────────┐│   └── actions/                           # Composite actions

│ 2. Select Scanner (Snyk, npm-audit, pip-audit, etc.)       ││       ├── scan-vulnerabilities/          # Multi-language scanning

└─────────────────────────────────────────────────────────────┘│       ├── process-vulnerabilities/       # Results processing

                            ↓│       └── create-security-issue/         # GitHub issue creation

┌─────────────────────────────────────────────────────────────┐│

│ 3. Install Dependencies & Run Scan                          │├── README.md                              # This file

└─────────────────────────────────────────────────────────────┘├── CONTRIBUTING.md                        # Contribution guidelines

                            ↓└── LICENSE                                # MIT License

┌─────────────────────────────────────────────────────────────┐```

│ 4. Process & Normalize Results                              │

└─────────────────────────────────────────────────────────────┘## 🎨 Supported Languages & Scanners

                            ↓

┌─────────────────────────────────────────────────────────────┐| Language | Auto-Detected Files | Default Scanner | Alternative Scanners |

│ 5. Create GitHub Issue with Fix Commands                    │|----------|-------------------|-----------------|---------------------|

└─────────────────────────────────────────────────────────────┘| **Node.js** | `package.json` | Snyk / npm-audit | - |

                            ↓| **Python** | `requirements.txt`, `setup.py`, `pyproject.toml` | Snyk / pip-audit | - |

┌─────────────────────────────────────────────────────────────┐| **Rust** | `Cargo.toml` | cargo-audit | - |

│ 6. Assign to GitHub Copilot for AI-Powered Fixes           │| **Scala** | `build.sbt`, `build.sc` | Snyk / Trivy | - |

└─────────────────────────────────────────────────────────────┘| **Java** | `pom.xml`, `build.gradle` | Snyk / OWASP Dependency Check | - |

```| **Go** | `go.mod` | govulncheck | - |

| **.NET** | `*.csproj`, `*.sln` | dotnet list | - |

## Configuration Options| **Ruby** | `Gemfile` | bundler-audit | - |

| **PHP** | `composer.json` | composer-audit | - |

### Inputs

## 📚 Usage Examples

| Input | Description | Default |

|-------|-------------|---------|### Basic Usage (Auto-Detection)

| `language` | Programming language (`auto`, `nodejs`, `python`, `rust`, `scala`, `java`, `go`, `dotnet`, `ruby`, `php`) | `auto` |

| `scanner` | Scanner tool (`auto`, `snyk`, `npm-audit`, `pip-audit`, `cargo-audit`, `trivy`, etc.) | `auto` |```yaml

| `severity-threshold` | Minimum severity (`low`, `medium`, `high`, `critical`) | `low` |jobs:

| `working-directory` | Directory to scan | `.` |  scan:

| `create-issue` | Create GitHub issue | `true` |    uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main

    secrets:

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
