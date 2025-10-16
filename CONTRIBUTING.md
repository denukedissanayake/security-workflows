# Contributing to Security Workflows

Thank you for your interest in contributing to this centralized security workflows repository! 🎉

## 🌟 How to Contribute

We welcome contributions of all kinds:

- 🐛 Bug fixes
- ✨ New features
- 📝 Documentation improvements
- 🎨 Example workflows
- 🔧 Tool support additions
- 💡 Ideas and suggestions

## 🚀 Getting Started

### 1. Fork the Repository

Click the "Fork" button at the top of this repository to create your own copy.

### 2. Clone Your Fork

```bash
git clone https://github.com/YOUR_USERNAME/security-workflows.git
cd security-workflows
```

### 3. Create a Branch

```bash
git checkout -b feature/your-feature-name
```

Use descriptive branch names:
- `feature/add-ruby-support`
- `fix/snyk-token-validation`
- `docs/improve-examples`
- `refactor/simplify-scanning-logic`

## 📋 Contribution Guidelines

### Code Contributions

#### For Workflow Changes

1. **Test thoroughly**: Test your changes with multiple languages and scenarios
2. **Document inputs/outputs**: Update YAML comments and README files
3. **Maintain backward compatibility**: Don't break existing usage patterns
4. **Follow GitHub Actions best practices**: Use proper error handling, logging, etc.

#### For Action Changes

1. **Update branding**: Ensure `action.yml` has appropriate icons and colors
2. **Document all inputs**: Include descriptions, defaults, and whether they're required
3. **Test with different scanners**: Verify compatibility across tools
4. **Add error handling**: Gracefully handle missing dependencies or failures

#### For Documentation

1. **Be clear and concise**: Use simple language
2. **Include examples**: Show real-world usage
3. **Keep it updated**: Ensure docs match the current code
4. **Use proper formatting**: Follow Markdown conventions

### Adding Language Support

To add support for a new programming language:

1. **Update `scan-vulnerabilities/action.yml`**:
   - Add language detection logic
   - Add scanner selection logic
   - Add dependency installation logic
   - Add scanning logic

2. **Update `process-vulnerabilities/action.yml`**:
   - Add fix command prefix for the language
   - Add normalization logic if using a new scanner format

3. **Update `create-security-issue/action.yml`**:
   - Add language-specific fix command generation

4. **Update documentation**:
   - Add to supported languages table in README
   - Create an example workflow
   - Update troubleshooting section

5. **Test thoroughly**:
   - Create a test repository with the new language
   - Run the workflow and verify all steps work
   - Ensure issues are created with correct fix commands

### Adding Scanner Support

To add support for a new security scanner:

1. **Update detection logic** in `scan-vulnerabilities/action.yml`
2. **Add installation steps** for the scanner
3. **Add scanning command** and output handling
4. **Add normalization logic** to convert scanner output to common format
5. **Document** the scanner in README and examples
6. **Test** with multiple projects

## 🧪 Testing Your Changes

### Local Testing

Before submitting, test your changes locally:

1. **Create a test repository** with the language/framework you're targeting
2. **Copy your modified workflows/actions** to the test repo
3. **Update paths** to use local actions (`./.github/actions/...`)
4. **Run the workflow** and verify all steps complete successfully
5. **Check outputs**: Verify scan results, issues, and artifacts are correct

### Test Checklist

- [ ] Workflow runs without errors
- [ ] Language auto-detection works correctly
- [ ] Scanner selection is appropriate
- [ ] Scan results are normalized correctly
- [ ] GitHub issue is created with proper format
- [ ] Fix commands are accurate for the language
- [ ] Artifacts are uploaded correctly
- [ ] Summary is displayed in GitHub Actions UI

## 📝 Pull Request Process

1. **Update documentation**: Ensure README, examples, and comments are updated
2. **Test your changes**: Follow the testing checklist above
3. **Commit with clear messages**:
   ```bash
   git commit -m "feat: add Rust support with cargo-audit"
   git commit -m "fix: handle empty scan results gracefully"
   git commit -m "docs: add Java Maven example workflow"
   ```

4. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Create a Pull Request**:
   - Go to the original repository
   - Click "New Pull Request"
   - Select your fork and branch
   - Fill out the PR template
   - Link any related issues

### PR Template

```markdown
## Description
Brief description of your changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Breaking change

## Testing
Describe how you tested your changes

## Checklist
- [ ] Code follows the project style
- [ ] Documentation updated
- [ ] All tests pass
- [ ] Examples added/updated if needed
```

## 🎨 Code Style

### YAML Style

- Use 2 spaces for indentation
- Use single quotes for strings (when quotes are needed)
- Add comments to explain complex logic
- Keep lines under 100 characters when possible

### Shell Script Style

- Use `bash` for shell scripts
- Add comments for complex operations
- Use meaningful variable names (UPPERCASE for environment variables)
- Handle errors gracefully with appropriate logging

### Documentation Style

- Use clear, simple language
- Include code examples
- Use emojis sparingly for visual organization
- Keep table of contents updated
- Use proper Markdown formatting

## 🐛 Reporting Bugs

Found a bug? Please [create an issue](https://github.com/denukedissanayake/security-workflows/issues/new) with:

- **Clear title**: Describe the issue concisely
- **Description**: What happened vs. what you expected
- **Steps to reproduce**: How to recreate the issue
- **Environment**: Language, scanner, GitHub Actions runner
- **Logs**: Relevant workflow logs (sanitize sensitive data!)
- **Screenshots**: If applicable

## 💡 Suggesting Features

Have an idea? [Open a discussion](https://github.com/denukedissanayake/security-workflows/discussions/new) or issue with:

- **Use case**: Why is this needed?
- **Proposed solution**: How should it work?
- **Alternatives**: Other approaches you considered
- **Examples**: Show how it would be used

## 📜 Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for everyone.

### Our Standards

**Positive behavior includes:**
- Being respectful and inclusive
- Accepting constructive criticism gracefully
- Focusing on what's best for the community
- Showing empathy towards others

**Unacceptable behavior includes:**
- Harassment, trolling, or insulting comments
- Personal or political attacks
- Publishing others' private information
- Any conduct inappropriate in a professional setting

### Enforcement

Instances of unacceptable behavior may be reported to the project maintainers. All complaints will be reviewed and investigated promptly and fairly.

## 🏆 Recognition

Contributors will be:
- Listed in our README (if you want!)
- Mentioned in release notes
- Given credit in commit messages

## 📞 Getting Help

Need help contributing?

- 💬 [GitHub Discussions](https://github.com/denukedissanayake/security-workflows/discussions)
- 📧 Open an issue with the `question` label
- 📖 Check existing documentation and examples

## 🙏 Thank You!

Every contribution, no matter how small, helps make this project better. Thank you for being part of the community!

---

**Happy Contributing! 🚀**
