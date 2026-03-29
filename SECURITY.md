# Security Policy

## 🔒 ASI Alliance Wallet Security

Security is paramount for ASI Alliance Wallet and the Fetch.ai ecosystem. This document outlines comprehensive security procedures, incident response protocols, and compliance requirements (PCI-DSS 12.10.1).

---

## 🚨 CRITICAL SECURITY ALERT

### Recent Supply Chain Attack Detection

**Date:** February 10, 2026  
**Status:** ACTIVE THREAT MITIGATED

**Summary:** Automated security bots attempted to inject non-existent axios version 1.13.5 into the dependency tree. This version does not exist in the official npm registry and represents a potential supply chain attack.

**Action Taken:** All suspicious PRs identified and blocked. See `SECURITY_AUDIT_REPORT.md` for details.

**User Action Required:** None - repository maintainers are managing the response.

---

## 📋 Table of Contents

1. [Supported Versions](#supported-versions)
2. [Reporting a Vulnerability](#reporting-a-vulnerability)
3. [Incident Response Plan](#incident-response-plan-pci-dss-12101)
4. [Security Classification](#security-classification)
5. [Response Timelines](#response-timelines)
6. [Disclosure Policy](#disclosure-policy)
7. [Security Best Practices](#security-best-practices)
8. [Compliance](#compliance)

---

## 🛡️ Supported Versions

We actively maintain security updates for the following versions:

| Version | Supported          | End of Life |
| ------- | ------------------ | ----------- |
| 1.x.x   | ✅ Active Support  | TBD         |
| 0.12.x  | ⚠️ Security Only   | Jun 2026    |
| < 0.12  | ❌ No Support      | Ended       |

**Recommendation:** Always use the latest stable version for security updates.

---

## 🚨 Reporting a Vulnerability

### Quick Report

**For urgent security issues:**

📧 **Email:** security@fetch.ai  
📱 **Emergency:** Use PagerDuty for critical incidents  
🔒 **Encryption:** Use our PGP key for sensitive reports

### Detailed Reporting Process

#### Step 1: Classify the Vulnerability

**CRITICAL** - Immediate threat to user funds or data:
- Private key exposure
- Remote code execution
- Authentication bypass
- SQL injection
- Prototype pollution with exploit path

**HIGH** - Significant security impact:
- Cross-site scripting (XSS)
- Authorization bypass
- Information disclosure
- Dependency vulnerabilities (CVSS 7.0+)

**MEDIUM** - Moderate security impact:
- CSRF vulnerabilities
- Insecure defaults
- Missing security headers
- Dependency vulnerabilities (CVSS 4.0-6.9)

**LOW** - Minor security concerns:
- Informational leakage
- Best practice violations
- Documentation issues

#### Step 2: Prepare Your Report

**Required Information:**

```markdown
## Vulnerability Report Template

### Classification
[CRITICAL/HIGH/MEDIUM/LOW]

### Title
[Short descriptive title]

### Description
[Detailed description of the vulnerability]

### Impact
[What can an attacker do? What is at risk?]

### Reproduction Steps
1. [Step 1]
2. [Step 2]
3. [Step 3]
...

### Proof of Concept
[Code, screenshots, or video demonstrating the issue]

### Affected Versions
[Which versions are vulnerable?]

### Environment
- OS: [e.g., Ubuntu 22.04]
- Node Version: [e.g., 18.x]
- Browser: [if applicable]
- Additional dependencies: [list]

### Suggested Fix
[If you have a proposed solution]

### References
[CVE numbers, related vulnerabilities, research papers]

### Contact Information
[Your name/handle and contact method for follow-up]
```

#### Step 3: Send Securely

**Email:** security@fetch.ai  
**Subject Format:** `[CLASSIFICATION] Short Title`

**Example:**
```
Subject: [CRITICAL] Private Key Exposure via Memory Leak
```

**For encrypted communication:**

```bash
# Download our PGP key
curl https://fetch.ai/security-pgp.key | gpg --import

# Encrypt your report
gpg --encrypt --armor -r security@fetch.ai report.txt
```

---

## 🔄 Incident Response Plan (PCI-DSS 12.10.1)

### Phase 1: Detection & Classification (0-1 hour)

**Objective:** Identify and classify the security incident

**Actions:**
1. **Receive & Acknowledge**
   - Security team receives vulnerability report
   - Auto-acknowledge receipt within 15 minutes
   - Assign incident ID: `SEC-YYYY-MM-NNNN`

2. **Initial Assessment**
   - Verify the vulnerability exists
   - Confirm affected versions
   - Classify severity using matrix

3. **Activate Response Team**
   - CRITICAL: Immediate escalation to security lead
   - HIGH: Escalate within 1 hour
   - MEDIUM: Escalate within 4 hours
   - LOW: Regular triage queue

**Responsible:** Security Triage Team

### Phase 2: Containment (1-24 hours)

**Objective:** Prevent further exploitation

**Actions:**

**For CRITICAL incidents:**
1. **Immediate Actions**
   - Disable affected functionality if possible
   - Deploy WAF rules to block exploitation attempts
   - Enable enhanced monitoring and alerting
   - Notify key stakeholders

2. **Communication**
   - Internal: Security team, engineering leads, executives
   - External: Prepare user notification (if needed)
   - Compliance: Notify compliance officer if PII/PCI involved

**For HIGH incidents:**
1. Emergency patch development begins
2. Enhanced monitoring deployed
3. Incident response team mobilized

**For MEDIUM/LOW incidents:**
1. Add to security sprint backlog
2. Standard monitoring
3. Schedule fix for next release

**Responsible:** Incident Response Team

### Phase 3: Eradication (24-72 hours)

**Objective:** Develop and test security fix

**Actions:**
1. **Fix Development**
   - Create security patch
   - Conduct code review
   - Run security testing suite
   - Perform regression testing

2. **Documentation**
   - Document root cause
   - Update security advisory
   - Prepare release notes
   - Update this security policy if needed

3. **Validation**
   - Verify fix addresses vulnerability
   - Confirm no new issues introduced
   - Test across all supported versions

**Responsible:** Engineering Team + Security Team

### Phase 4: Recovery (72 hours+)

**Objective:** Deploy fix and restore normal operations

**Actions:**
1. **Deployment**
   - Release security patch
   - Update documentation
   - Publish security advisory
   - Notify affected users

2. **Verification**
   - Monitor for successful patch adoption
   - Verify exploitation attempts cease
   - Confirm system stability

3. **Communication**
   - Public disclosure (for non-critical issues)
   - Credit researcher (if applicable)
   - Update CVE database
   - Post-incident report

**Responsible:** Release Team + Communications

### Phase 5: Lessons Learned (7-14 days)

**Objective:** Improve security posture

**Actions:**
1. **Post-Incident Review**
   - Conduct retrospective meeting
   - Document timeline and actions
   - Identify what worked / what didn't
   - Update incident response procedures

2. **Process Improvements**
   - Update security testing
   - Add new security controls
   - Enhance monitoring
   - Provide security training

3. **Reporting**
   - Internal incident report
   - Compliance reporting (if required)
   - Update metrics and KPIs

**Responsible:** Security Team Lead

---

## 📊 Security Classification

### CRITICAL (CVSS 9.0-10.0)

**Response Time:** Immediate (< 1 hour)  
**Fix Timeline:** Emergency patch within 24 hours  
**Disclosure:** After patch deployment + 7 days

**Examples:**
- Remote code execution
- Private key/credential theft
- Complete authentication bypass
- Mass data breach
- Wormable vulnerabilities

**Incident Team:**
- Security Lead (Incident Commander)
- CTO / Engineering VP
- Senior Engineers (2+)
- Communications Lead
- Legal Counsel

### HIGH (CVSS 7.0-8.9)

**Response Time:** < 4 hours  
**Fix Timeline:** Patch within 7 days  
**Disclosure:** After patch + 14 days

**Examples:**
- Privilege escalation
- SQL injection
- Authentication weaknesses
- Sensitive data exposure
- Cryptographic failures

**Incident Team:**
- Security Lead
- Engineering Lead
- 1-2 Engineers
- Product Manager

### MEDIUM (CVSS 4.0-6.9)

**Response Time:** < 1 business day  
**Fix Timeline:** Next regular release (2-4 weeks)  
**Disclosure:** With release notes

**Examples:**
- CSRF vulnerabilities
- XSS (non-persistent)
- Information disclosure (limited)
- Insecure defaults
- Missing security headers

**Incident Team:**
- Security Engineer
- Assigned Developer
- QA Lead

### LOW (CVSS 0.1-3.9)

**Response Time:** < 1 week  
**Fix Timeline:** Opportunistic (next release)  
**Disclosure:** Standard release notes

**Examples:**
- Best practice violations
- Minor information leakage
- Documentation issues
- Low-risk misconfigurations

**Incident Team:**
- Security Engineer
- Developer (as available)

---

## ⏱️ Response Timelines

| Severity | Acknowledgment | Initial Assessment | Fix Development | Patch Deployment | Public Disclosure |
|----------|----------------|-------------------|-----------------|------------------|------------------|
| CRITICAL | 15 minutes | 1 hour | 4-24 hours | 24-48 hours | Patch + 7 days |
| HIGH | 2 hours | 4 hours | 1-7 days | 7-14 days | Patch + 14 days |
| MEDIUM | 1 business day | 2 business days | 2-4 weeks | Next release | With release |
| LOW | 1 week | 1 week | Opportunistic | Next release | With release |

**Note:** Timelines may be adjusted based on:
- Exploit complexity
- Attack surface
- User impact
- Available resources
- Coordination with other vendors

---

## 📢 Disclosure Policy

### Coordinated Disclosure

We follow responsible disclosure practices:

1. **Private Reporting**
   - Report received and acknowledged
   - Investigation and fix development
   - Testing and validation
   - Patch deployment

2. **Coordinated Release**
   - 90-day disclosure window (for non-critical)
   - 7-day window for critical with active exploitation
   - Coordinate with CVE program
   - Credit researchers (with permission)

3. **Public Disclosure**
   - Security advisory published
   - CVE entry created
   - Release notes updated
   - Community notification

### Public Disclosure Guidelines

**Please DO:**
- Report privately first
- Allow reasonable time for patching
- Coordinate disclosure timing
- Provide technical details
- Accept recognition gracefully

**Please DON'T:**
- Publicly disclose before patch
- Attack production systems
- Access user data without permission
- Demand unreasonable payment
- Use vulner abilities for malicious purposes

### Researcher Recognition

We maintain a Hall of Fame for security researchers:

**Recognition Options:**
- Public acknowledgment (with permission)
- CVE credit
- Hall of Fame listing
- Swag and merchandise
- Conference ticket sponsorship (for significant finds)

**Note:** We do not currently offer a bug bounty program.

---

## 🔐 Security Best Practices

### For Users

1. **Keep Software Updated**
   ```bash
   # Check current version
   npm list @asi-alliance/wallet
   
   # Update to latest
   npm update @asi-alliance/wallet
   ```

2. **Verify Package Integrity**
   ```bash
   # Verify package signatures
   npm audit signatures
   
   # Check for known vulnerabilities
   npm audit
   ```

3. **Secure Private Keys**
   - Never commit private keys to repositories
   - Use hardware wallets for significant holdings
   - Enable 2FA on all accounts
   - Use encrypted storage

4. **Monitor Security Advisories**
   - Watch this repository for security updates
   - Subscribe to security mailing list
   - Follow @FetchAI on Twitter for alerts

### For Developers

1. **Dependency Management**
   ```bash
   # Use lock files
   npm ci  # Don't use npm install in CI/CD
   
   # Regular audits
   npm audit
   npm audit fix
   
   # Automated updates (Dependabot enabled)
   ```

2. **Secure Coding**
   - Follow OWASP Top 10 guidelines
   - Use parameterized queries (prevent SQL injection)
   - Validate all inputs
   - Escape all outputs
   - Use security linters (ESLint security plugins)

3. **Code Review**
   - All code requires review (enforced by CODEOWNERS)
   - Security-sensitive changes require security team review
   - Run SAST tools before merge

4. **Testing**
   ```bash
   # Security tests
   npm run test:security
   
   # Integration tests
   npm run test:integration
   
   # Coverage requirements
   npm run test:coverage  # Must maintain >80%
   ```

### For Operators

1. **Infrastructure Security**
   - Use TLS 1.3 for all communications
   - Implement Web Application Firewall (WAF)
   - Enable DDoS protection
   - Regular security scanning

2. **Monitoring & Alerting**
   - Deploy security monitoring (SIEM)
   - Alert on anomalous behavior
   - Log all security events
   - Retain logs for 90 days minimum

3. **Access Control**
   - Implement least privilege
   - Regular access reviews
   - Multi-factor authentication required
   - Separate production/development access

4. **Incident Response**
   - Maintain incident response plan
   - Regular tabletop exercises
   - On-call security rotation
   - Post-incident reviews

---

## ✅ Compliance

### PCI-DSS Requirements

This security policy addresses the following PCI-DSS requirements:

- **12.10.1:** Incident response plan (✅ Implemented)
- **12.10.2:** Review and test incident response plan (Annually)
- **12.10.3:** Designate staff for incident response (Security Team)
- **12.10.4:** Training for incident response (Quarterly)
- **12.10.5:** Security monitoring (24/7)
- **12.10.6:** Modify incident response based on lessons learned

### Compliance Documentation

**Available Documents:**
- Incident Response Plan (this document)
- Security Controls Matrix (`docs/compliance/controls.md`)
- Audit Trail Procedures (`docs/compliance/audit-trail.md`)
- Data Retention Policy (`docs/compliance/retention.md`)

### Audit Support

For compliance audits:
- Contact: compliance@fetch.ai
- Documentation available upon request
- Evidence collection assistance provided
- Audit findings tracked and remediated

---

## 📞 Contact Information

### Security Team

**General Security:** security@fetch.ai  
**Emergency:** PagerDuty (for authorized personnel)  
**PGP Key:** https://fetch.ai/security-pgp.key  
**Key Fingerprint:** `[PGP fingerprint would go here]`

### Compliance

**Compliance Officer:** compliance@fetch.ai  
**Privacy/GDPR:** privacy@fetch.ai  
**Audit Requests:** audit@fetch.ai

### Communication Channels

**GitHub Security Advisory:** Use this repository's security advisory feature  
**Twitter:** @FetchAI (for public security announcements)  
**Discord:** (for community security discussions - not for reporting)

---

## 🔄 Policy Updates

**Last Updated:** February 10, 2026  
**Version:** 2.0  
**Next Review:** May 10, 2026

**Changelog:**
- **v2.0 (Feb 2026):** Added PCI-DSS 12.10.1 incident response procedures, supply chain attack documentation
- **v1.1 (Dec 2025):** Enhanced classification matrix
- **v1.0 (Jun 2025):** Initial security policy

**Review Schedule:**
- Quarterly review of procedures
- Annual comprehensive update
- As-needed updates for new threats

---

## 🙏 Acknowledgments

We thank the security research community for helping keep ASI Alliance Wallet secure.

### Security Researchers Hall of Fame

**2026:**
- [To be updated as researchers are credited]

**2025:**
- [Historical credits]

---

## 📚 Additional Resources

- **Security Audit Report:** `SECURITY_AUDIT_REPORT.md`
- **Dependency Security:** `.github/dependabot.yml`
- **Code Ownership:** `.github/CODEOWNERS`
- **Contributing Guidelines:** `CONTRIBUTING.md`
- **Code of Conduct:** `CODE_OF_CONDUCT.md`

---

**Thank you for helping keep ASI Alliance Wallet secure! 🔒**

*For suggestions on improving this security policy, please submit a pull request or contact security@fetch.ai*
