# Pull Request

## 📝 Proposed Changes

_[Provide a clear and concise description of the changes in this pull request]_

---

## 🔗 Linked Issues

_[Link to related issues using keywords like "Fixes #123" or "Closes #456"]_

- Fixes #
- Related to #

---

## 🏷️ Types of Changes

_What type of change does this pull request make? (Check all that apply)_

- [ ] 🐛 Bug fix (non-breaking change that fixes an issue)
- [ ] ✨ New feature (non-breaking change that adds functionality)
- [ ] 🚨 Breaking change (fix or feature that would cause existing functionality to stop working as expected)
- [ ] 📝 Documentation update
- [ ] 🛠️ Refactoring (no functional changes)
- [ ] ⚡ Performance improvement
- [ ] 🔒 Security fix
- [ ] 📦 Dependency update
- [ ] 🧪 Tests (adding or updating tests)
- [ ] 🔧 Build/Infrastructure changes

---

## 🔒 Security Impact Assessment (PCI-DSS 6.4.5)

_**REQUIRED:** All PRs must assess security impact_

### Does this PR affect any security-sensitive areas?

- [ ] 🔑 Private key handling or cryptography
- [ ] 🔐 Authentication or authorization
- [ ] 📝 Transaction signing
- [ ] 🌐 Network communication or API calls
- [ ] 💾 Data storage or encryption
- [ ] 🛡️ Input validation or sanitization
- [ ] 👥 User permissions or access control
- [ ] ❌ None of the above (low security impact)

### Security Testing Performed

- [ ] Ran security-specific tests (`npm run test:security`)
- [ ] Reviewed for injection vulnerabilities (SQL, XSS, etc.)
- [ ] Verified input validation and output encoding
- [ ] Checked for sensitive data exposure
- [ ] Tested authentication/authorization flows
- [ ] Reviewed cryptographic implementations
- [ ] ❌ Not applicable (documentation/config only)

### Vulnerability Scan Results

```bash
# Run and paste results:
# npm audit
# npm audit signatures
```

_[Paste npm audit results here or state "No new vulnerabilities"]_

---

## 📦 Dependency Changes (PCI-DSS 6.2)

_**REQUIRED** if dependencies are modified_

### Dependencies Added/Updated/Removed

```json
// List changes from package.json
{
  "added": [
    // "package-name@version"
  ],
  "updated": [
    // "package-name: 1.0.0 → 1.1.0"
  ],
  "removed": [
    // "package-name@version"
  ]
}
```

### Dependency Security Verification

- [ ] Verified package exists in official npm registry
- [ ] Checked package maintainer reputation
- [ ] Reviewed package changelog/release notes
- [ ] Verified no known CVEs for new versions
- [ ] Confirmed integrity checksums match
- [ ] Tested with updated dependencies locally
- [ ] Updated lock files (package-lock.json / yarn.lock)

### Supply Chain Attack Prevention

⚠️ **CRITICAL:** Verify version numbers exist before merging!

```bash
# For each updated package, verify version exists:
npm view package-name@version

# Example for axios:
npm view axios@1.7.9  # ✅ Valid
npm view axios@1.13.5 # ❌ INVALID - Supply chain attack!
```

- [ ] Manually verified all version numbers exist in registry
- [ ] No suspicious version jumps or non-existent versions
- [ ] Dependabot PR reviewed by human (not auto-merged)

---

## 🚧 Breaking Changes

_**REQUIRED** if you checked "Breaking change" above_

### What breaks?

_[Describe what existing functionality will stop working]_

### Migration Guide

_[Provide step-by-step instructions for users to migrate]_

```typescript
// Before (old code)

// After (new code)
```

### Deprecation Timeline

- [ ] Old API deprecated in this version
- [ ] Old API will be removed in version: `___`
- [ ] Migration documentation added
- [ ] Changelog updated with breaking changes

---

## ✅ Checklist

### Required for All PRs

- [ ] I have read the [CONTRIBUTING](https://github.com/fetchai/fetch-wallet/blob/main/CONTRIBUTING.md) guide
- [ ] I have read and understood the [SECURITY](./SECURITY.md) policy
- [ ] My code follows the project's code style
- [ ] Checks and tests pass locally with my changes
- [ ] I have rebased my branch on the latest main
- [ ] My commit messages follow the [conventional commits](https://www.conventionalcommits.org/) format

### Code Quality

- [ ] I have performed a self-review of my own code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] My changes generate no new warnings or errors
- [ ] I have removed any debug logging or console statements
- [ ] I have followed security best practices

### Testing

- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
- [ ] I have added integration tests (if applicable)
- [ ] I have tested on multiple browsers (for frontend changes)
- [ ] I have tested on mobile devices (if applicable)
- [ ] I have checked that code coverage does not decrease

### Documentation

- [ ] I have updated the documentation (if applicable)
- [ ] I have updated the README (if applicable)
- [ ] I have added/updated JSDoc comments for new functions
- [ ] I have updated the changelog (CHANGELOG.md)
- [ ] I have updated API documentation (if applicable)

### Security & Compliance

- [ ] I have completed the Security Impact Assessment section above
- [ ] I have verified all dependency changes (if applicable)
- [ ] I have not committed sensitive data (keys, tokens, passwords)
- [ ] I have not introduced any known security vulnerabilities
- [ ] I have followed PCI-DSS requirements (if applicable)

### For Security-Critical Changes

_Only required if you checked any security-sensitive areas above_

- [ ] Security team has been notified (@RemyLoveLogicAI or @agent-dominatrix)
- [ ] Security-specific tests added/updated
- [ ] Cryptographic implementations reviewed by security team
- [ ] Threat model updated (if applicable)
- [ ] Security audit completed (for major changes)

---

## 📸 Screenshots / Videos

_[If applicable, add screenshots or videos to demonstrate the changes]_

### Before

_[Screenshot/description of behavior before changes]_

### After

_[Screenshot/description of behavior after changes]_

---

## 🧪 Test Coverage

```bash
# Paste test coverage report
# npm run test:coverage
```

### Coverage Summary

| Type | Coverage | Change |
|------|----------|--------|
| Statements | __% | __% |
| Branches | __% | __% |
| Functions | __% | __% |
| Lines | __% | __% |

_**Note:** Coverage should not decrease. Target: >80% overall_

---

## 🚀 Deployment Notes

_[Any special instructions for deployment? Environment variables, database migrations, etc.]_

### Pre-deployment Checklist

- [ ] Database migrations prepared (if applicable)
- [ ] Environment variables documented
- [ ] Rollback plan documented
- [ ] Monitoring/alerts configured
- [ ] Feature flags configured (if applicable)

### Post-deployment Verification

- [ ] Smoke tests defined
- [ ] Health check endpoints verified
- [ ] Rollback triggers defined
- [ ] Monitoring dashboards updated

---

## 💬 Further Comments

_[If this is a relatively large or complex change, explain your approach, alternatives you considered, design decisions, etc.]_

### Design Decisions

_[Explain key design decisions and tradeoffs]_
### Alternatives Considered

_[What other approaches did you consider and why did you choose this one?]_

### Technical Debt

_[Does this PR introduce or address technical debt? Explain.]_

### Performance Considerations

_[How does this affect performance? Any benchmarks?]_

---

## 🔍 Reviewer Guidelines

### What to Review

**Security Reviewers:**
- [ ] All security checkboxes verified
- [ ] No sensitive data exposure
- [ ] Input validation adequate
- [ ] Cryptography implementations sound
- [ ] Dependency changes legitimate

**Code Reviewers:**
- [ ] Code follows style guide
- [ ] Tests are comprehensive
- [ ] Documentation is clear
- [ ] No obvious bugs or issues
- [ ] Performance is acceptable

**Compliance Reviewers:**
- [ ] PCI-DSS requirements met
- [ ] Change documentation adequate
- [ ] Audit trail maintained
- [ ] Access controls enforced

---

## ⚠️ Security Incident Response

_**IF THIS PR FIXES A SECURITY VULNERABILITY:**_

1. **Do not disclose details in this PR description**
2. Reference the private security advisory: `GHSA-____`
3. Follow [Security Policy](./SECURITY.md) disclosure timeline
4. Coordinate release with security team
5. Prepare security advisory for publication

**Security Advisory Template:** See `SECURITY.md`

---

## ℹ️ Additional Information

**Related Documentation:**
- Security Policy: [SECURITY.md](./SECURITY.md)
- Security Audit: [SECURITY_AUDIT_REPORT.md](./SECURITY_AUDIT_REPORT.md)
- Contributing Guide: [CONTRIBUTING.md](./CONTRIBUTING.md)
- Code of Conduct: [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)

**Need Help?**
- 💬 Ask in PR comments
- 📧 Email: security@fetch.ai (for security questions)
- 👥 Discord: [Community channel]
- 📖 Docs: [Documentation site]

---

**Thank you for contributing to ASI Alliance Wallet! 🚀**

_By submitting this pull request, I confirm that my contribution is made under the terms of the repository's license and I have followed all security and compliance requirements._
