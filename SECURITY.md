# Security Policy

## Supported Versions

Security fixes are applied to the latest version on the `main` branch.

## Reporting a Vulnerability

Please do not open a public GitHub issue for a suspected security vulnerability.

Instead, use GitHub's private vulnerability reporting/security advisory features for this repository when available. If private reporting is unavailable, contact the repository owner through a private GitHub channel and include:

- A description of the issue
- The affected file and version/commit
- Steps needed to reproduce it
- Any potential impact

Do not include passwords, access tokens, Home Assistant secrets, notification credentials, or other sensitive information in a public issue or pull request.

## Repository Security Rules

This project is intended to contain reusable Home Assistant blueprint code only. It must not contain:

- Home Assistant `secrets.yaml`
- Access tokens or API keys
- Passwords or credentials
- Personal Home Assistant backups or `.storage/` data
- Private device identifiers or unrelated personal configuration

Secret scanning and push protection should remain enabled for this repository.
