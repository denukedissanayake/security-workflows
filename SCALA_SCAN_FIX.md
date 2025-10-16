# Scala Security Scan Fix

## Problem
The security scan workflow was detecting Scala projects correctly but finding 0 vulnerabilities because:

1. **SBT (Scala Build Tool) was not installed** - GitHub Actions runners don't have SBT pre-installed
2. **Dependencies couldn't be resolved** - Without SBT, the workflow couldn't download project dependencies
3. **Snyk had nothing to scan** - Without a dependency tree, vulnerability scanners found nothing

## What Was Fixed

### 1. Added Java and SBT Setup (Lines 192-211)
```yaml
- name: Set up Java and SBT (if needed for Scala/Java)
  if: steps.detect.outputs.language == 'scala' || steps.detect.outputs.language == 'java'
  uses: actions/setup-java@v4
  with:
    distribution: 'temurin'
    java-version: '11'

- name: Set up SBT (if needed for Scala)
  if: steps.detect.outputs.language == 'scala'
  shell: bash
  run: |
    echo "INFO: Installing SBT"
    echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | sudo tee /etc/apt/sources.list.d/sbt.list
    echo "deb https://repo.scala-sbt.org/scalasbt/debian /" | sudo tee /etc/apt/sources.list.d/sbt_old.list
    curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
    sudo apt-get update
    sudo apt-get install -y sbt
    sbt --version
```

**Why:** This installs Java (required for Scala) and SBT before attempting to resolve dependencies.

### 2. Improved Scala Dependency Resolution (Lines 245-253)
```yaml
scala)
  if [ -f "build.sbt" ]; then
    echo "INFO: Resolving SBT dependencies..."
    # First compile to ensure all dependencies are downloaded
    sbt compile -Dsbt.log.noformat=true || echo "WARNING: sbt compile failed, continuing anyway"
    # Also try to generate dependency tree
    sbt dependencyTree || echo "WARNING: Could not generate dependency tree"
  elif [ -f "build.sc" ]; then
    echo "INFO: Resolving Mill dependencies..."
    mill resolve _ || true
  fi
```

**Why:** 
- `sbt compile` downloads all dependencies (including transitive ones)
- `sbt dependencyTree` generates a complete dependency graph
- This ensures Snyk has the full dependency context to scan

### 3. Enhanced Snyk Scanning for Scala (Lines 318-343)
```yaml
if [ "$LANGUAGE" = "scala" ]; then
  snyk test --all-projects --json --severity-threshold=${{ inputs.severity-threshold }} > dependency-scan-results.json 2>&1 || true
else
  snyk test --json --severity-threshold=${{ inputs.severity-threshold }} > dependency-scan-results.json 2>&1 || true
fi

# Save raw Snyk results for debugging
cp dependency-scan-results.json snyk-results.json || true
```

**Why:**
- `--all-projects` flag tells Snyk to scan all SBT sub-projects
- Captures stderr output (`2>&1`) for better debugging
- Saves raw Snyk results for troubleshooting

## Testing the Fix

### Option 1: Test in Your Repository
1. Commit and push these changes to your `main` branch:
   ```bash
   cd /home/denuke/Work/Hackathon/security-workflows
   git add .github/actions/scan-vulnerabilities/action.yml
   git commit -m "Fix Scala security scanning - add SBT setup and improve dependency resolution"
   git push origin main
   ```

2. In your Scala application repository, trigger the workflow again

### Option 2: Test Locally (if you have a Scala project)
You can test the dependency resolution manually:
```bash
# Install SBT (Ubuntu/Debian)
echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | sudo tee /etc/apt/sources.list.d/sbt.list
curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
sudo apt-get update
sudo apt-get install sbt

# In your Scala project directory
sbt compile
sbt dependencyTree

# Install and run Snyk
npm install -g snyk
snyk auth YOUR_TOKEN
snyk test --all-projects
```

## Expected Results

After the fix, you should see:
- ✅ SBT successfully installed
- ✅ Dependencies resolved via `sbt compile`
- ✅ Snyk scanning with actual dependency data
- ✅ Vulnerabilities detected (if any exist in your dependencies)

## Common Issues

### If Still Finding 0 Vulnerabilities:
1. **Your project might actually be clean** - Check if dependencies have known vulnerabilities manually
2. **Snyk token might be invalid** - Verify token has correct permissions
3. **Project might be too old** - Ensure your Scala/SBT versions are supported by Snyk

### If Build Fails:
1. **Java version mismatch** - Adjust `java-version` in the setup step (try '8', '11', or '17')
2. **SBT version issues** - The script installs the latest; you may need a specific version
3. **Private dependencies** - If using private repos, add credentials configuration

## Alternative: Use Trivy Instead
If Snyk continues to have issues, you can switch to Trivy by modifying your workflow call:
```yaml
uses: denukedissanayake/security-workflows/.github/workflows/security-scan-reusable.yml@main
with:
  scanner: trivy  # Instead of 'auto' or 'snyk'
```

Trivy works without needing resolved dependencies in some cases.
