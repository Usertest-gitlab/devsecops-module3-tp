# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.x     | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

If you discover a security vulnerability in this project, please report it responsibly.

### How to Report

1. **DO NOT** create a public GitHub issue for security vulnerabilities
2. Send an email to: security@example.com
3. Include:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

### Response Timeline

- **Acknowledgment**: Within 48 hours
- **Initial assessment**: Within 5 business days
- **Resolution target**: Within 30 days for critical issues

### What to Expect

1. Acknowledgment of your report
2. Regular updates on the progress
3. Credit in the security advisory (if desired)
4. Notification when the fix is released

## Security Measures

This project implements the following security measures:

### Static Analysis (SAST)
- SonarQube for code quality and security
- Automated scanning on every pull request

### Dynamic Analysis (DAST)
- OWASP ZAP baseline scans
- Security headers verification

### Container Security
- Minimal base images (distroless)
- Non-root user execution
- Regular vulnerability scanning with Trivy
- No secrets in images

### CI/CD Security
- Minimal GITHUB_TOKEN permissions
- Secrets stored securely
- Pipeline fails on HIGH/CRITICAL vulnerabilities
- Deployment restricted to main branch

### Compliance
- SBOM generation (CycloneDX, SPDX)
- License verification
- Audit trail via GitHub Actions logs

## Security Contacts

- Security Team: security@example.com
- Project Maintainer: maintainer@example.com

---

*Last updated: January 2026*
