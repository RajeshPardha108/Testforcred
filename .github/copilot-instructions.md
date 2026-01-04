# Copilot Instructions for DevSecOps Credential Testing Repository

## Project Overview
This repository focuses on DevSecOps practices for detecting and preventing credential leaks in codebases using GitHub Actions workflows.

## Architecture
- **Workflows**: All CI/CD and security scanning logic resides in `.github/workflows/`
- **Main Workflow**: `main.yml` serves as the primary pipeline for credential testing
- **Test Files**: `Testfile.txt` contains sample content for testing scanning tools

## Key Patterns
- Use GitHub Actions for automated secret scanning on pushes and pull requests
- Integrate tools like TruffleHog or Gitleaks for comprehensive credential detection
- Follow DevSecOps principles: shift security left by scanning early in the pipeline

## Workflow Conventions
- Workflows trigger on `push` and `pull_request` events to the `main` branch
- Use official actions from `actions/checkout` for repository access
- Output security findings to GitHub Security tab or as workflow annotations

## Development Workflow
1. Edit workflows in `.github/workflows/main.yml`
2. Test locally using `act` CLI tool for GitHub Actions simulation
3. Commit and push to trigger automated scans

## Example Workflow Structure
```yaml
name: Credential Scan
on: [push, pull_request]
jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run TruffleHog
        uses: trufflesecurity/trufflehog@main
        with:
          path: ./
          base: main
          head: HEAD
```

## Security Best Practices
- Never commit actual credentials to the repository
- Use GitHub Secrets for storing API keys or tokens needed in workflows
- Regularly update scanning tools to detect new types of secrets

## File References
- [main.yml](.github/workflows/main.yml): Primary workflow file (currently minimal)
- [Testfile.txt](Testfile.txt): Sample file for testing scans