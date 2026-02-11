# Access Control Policy
## ASI Alliance Wallet Repository
**Version:** 1.0  
**Last Updated:** February 11, 2026  
**Compliance:** PCI-DSS 7.1, 7.2, 8.1, 8.2

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [Emergency Contacts](#emergency-contacts)
3. [Escalation Path](#escalation-path)
4. [Review Requirements](#review-requirements)
5. [Protection Rules](#protection-rules)
6. [Least Privilege](#least-privilege)
7. [Access Review](#access-review)
8. [Compliance](#compliance)

---

## 🎯 Overview

This document defines access control policies and procedures for the ASI Alliance Wallet repository. It complements the `.github/CODEOWNERS` file, which specifies technical ownership of code paths.

**Purpose:**
- Implement least privilege access control
- Ensure appropriate review for security-sensitive changes
- Maintain compliance with PCI-DSS requirements
- Provide clear escalation procedures

**Scope:**
- All repository contributors
- All code review processes
- All access management procedures
- All compliance requirements

---

## 📞 Emergency Contacts

### Security Emergencies

**Primary Contact:**
- GitHub: @RemyLoveLogicAI
- Role: Security Team Lead

**Secondary Contact:**
- GitHub: @agent-dominatrix
- Role: Security Engineer

**Emergency Email:**
- **See SECURITY.md for current contact information**
- ⚠️ Do not expose email addresses in code or documentation to prevent harvesting

**Emergency Escalation:**
- For critical security incidents: Use PagerDuty (authorized personnel only)
- After-hours incidents: Follow incident response plan in SECURITY.md

### General Questions

**Technical Lead:**
- GitHub: @sh-wallet
- Scope: Technical architecture, implementation questions

**Backend Lead:**
- GitHub: @AbbasAliLokhandwala
- Scope: Backend services, API integration

**Community:**
- Discord: ASI Alliance community server
- Telegram: ASI Alliance support group
- **Note:** Do not discuss security vulnerabilities in public channels

---

## 🔄 Escalation Path

### Standard Review Process

**Level 1: GitHub PR Review Request**
- Triggered automatically by CODEOWNERS
- Review within 2 business days
- Approval required before merge

**Level 2: Direct Mention in PR Comments**
- Use when review is time-sensitive
- Tag specific owners: @username
- Provide context for urgency

**Level 3: Email to Team**
- For issues requiring offline discussion
- Contact information in SECURITY.md
- Include PR link and summary

**Level 4: PagerDuty (Critical Issues Only)**
- **Only for:**
  - Active security exploits
  - Production outages
  - Critical compliance violations
  - Data breach incidents
- **Not for:**
  - Routine code reviews
  - Feature requests
  - General questions

### Incident Escalation

For security incidents, follow the incident response plan in `SECURITY.md`:

1. **Detection** (0-1 hour): Security team notified
2. **Classification** (1 hour): Severity assessed
3. **Containment** (1-24 hours): Threat mitigated
4. **Remediation** (24-72 hours): Fix developed and deployed
5. **Review** (7-14 days): Post-incident analysis

---

## ✅ Review Requirements

### Standard Pull Requests

**Minimum Requirements:**
- At least **1 approval** from CODEOWNERS
- All CI/CD checks must pass
- PR template completed (including security assessment)
- No merge conflicts

### Security-Critical Changes

**Enhanced Requirements:**
- At least **2 approvals** from CODEOWNERS
- **Mandatory approval** from security team (@RemyLoveLogicAI or @agent-dominatrix)
- Security testing completed and passed
- Security impact assessment documented

**Security-critical paths include:**
- `SECURITY.md`
- `.github/dependabot.yml`
- `.github/workflows/security*.yml`
- `packages/crypto/**`
- `packages/background/src/keyring/**`
- `packages/**/encryption/**`
- `packages/background/src/auth/**`
- `packages/**/signing/**`
- Any file handling private keys or cryptography

### Dependency Changes

**Special Requirements:**
- Security team review required
- Package version verification (must exist in official registry)
- npm audit results included in PR
- Supply chain attack verification completed
- Breaking change analysis if major version update

**Verification Checklist:**
```bash
# Verify package exists
npm view package-name@version

# Check for vulnerabilities
npm audit

# Verify signatures
npm audit signatures

# Review changelog
npm view package-name@version --json | jq .repository.url
```

### Breaking Changes

**Additional Requirements:**
- **All maintainers** must approve
- Migration guide required
- Deprecation timeline documented
- User communication plan
- Rollback plan documented

---

## 🔒 Protection Rules

### Main Branch Protection

**Requirements:**
- Protected branch status enabled
- Requires pull request reviews before merging
- Requires status checks to pass before merging
- Requires conversation resolution before merging
- Includes administrators (no bypass)

**Configuration:**
```bash
# Enable via GitHub CLI:
gh api repos/{owner}/{repo}/branches/main/protection \
  -X PUT \
  -f required_pull_request_reviews[required_approving_review_count]=2 \
  -f required_pull_request_reviews[require_code_owner_reviews]=true \
  -f required_pull_request_reviews[dismiss_stale_reviews]=true \
  -f enforce_admins=true
```

### Release Branches

**Additional Requirements:**
- Signed commits required
- Deploy key management procedures
- Version tagging required
- Changelog updates mandatory

### Security Branches

**Special Protection:**
- Security team access only
- No automated merges
- Manual deployment gates
- Enhanced audit logging

---

## 👥 Least Privilege

### Access Levels

**Read Access:**
- **Who:** All contributors
- **Can:** View code, create forks, open issues
- **Cannot:** Push to branches, merge PRs

**Write Access:**
- **Who:** Core team only (@RemyLoveLogicAI, @agent-dominatrix, @sh-wallet, @AbbasAliLokhandwala)
- **Can:** Create branches, push commits, approve PRs
- **Cannot:** Bypass branch protection, force push to main

**Admin Access:**
- **Who:** Repository owner only (@RemyLoveLogicAI)
- **Can:** Manage repository settings, configure integrations
- **Responsibilities:** Access reviews, security oversight, compliance

**Security Admin:**
- **Who:** Security team lead (@RemyLoveLogicAI, @agent-dominatrix)
- **Can:** Manage security settings, review security PRs
- **Responsibilities:** Security incident response, vulnerability management

### Permission Assignment

**Process:**
1. Request access via issue or email
2. Justification for access level required
3. Security team reviews request
4. Access granted for minimum required level
5. Access logged in audit trail

**Approval Authority:**
- Read access: Any core team member
- Write access: Security team + repository owner
- Admin access: Repository owner only

---

## 📅 Access Review

### Quarterly Access Review

**Schedule:** Every 90 days (March, June, September, December)

**Review Process:**
1. **List all collaborators:**
   ```bash
   gh api repos/{owner}/{repo}/collaborators --jq '.[].login'
   ```

2. **Review activity:**
   - Last commit date
   - Last PR review date
   - Last issue comment date

3. **Decision:**
   - Active users: Retain access
   - Inactive 90+ days: Remove access
   - Changed roles: Adjust permissions

4. **Documentation:**
   - Log all access changes
   - Update CODEOWNERS if needed
   - Notify affected users

**Responsible:** Security Team Lead (@RemyLoveLogicAI)

### Inactive Account Removal

**Policy:**
- Accounts inactive for **90+ days** are automatically flagged
- Security team reviews flagged accounts
- Access removed unless justified business need
- User notified before removal

**Re-activation:**
- User can request re-activation
- Must re-justify access need
- Same approval process as new access

### Emergency Access Revocation

**Immediate Revocation Triggers:**
- Security incident involving the account
- Suspected account compromise
- Policy violations
- Employment/contractor termination
- User request

**Procedure:**
1. Security team lead executes revocation
2. Remove from all repository permissions
3. Revoke API tokens and SSH keys
4. Notify affected user (unless security incident)
5. Document in audit trail
6. Review recent account activity

### Audit Trail

**Requirements:**
- All access changes logged
- Logs retained for 90 days minimum
- Monthly access report generated
- Quarterly compliance review

**Log Format:**
```
Date: 2026-02-11
Action: Access granted
User: username
Level: Write
Approved By: @RemyLoveLogicAI
Justification: Core team member for mobile development
```

---

## 📋 Compliance

### PCI-DSS Requirements

This access control policy addresses:

**PCI-DSS 7.1: Access Control Implementation**
- ✅ Limit access to system components and cardholder data
- ✅ Access granted based on job classification and function
- ✅ Default "deny-all" setting (Read-only for non-team members)

**PCI-DSS 7.2: Least Privilege Enforcement**
- ✅ Access rights assigned based on job duties
- ✅ Privileged access limited to minimum necessary
- ✅ Access granted for shortest time needed

**PCI-DSS 8.1: User Identification**
- ✅ Unique ID assigned before access granted (GitHub username)
- ✅ User identity verified before access grant
- ✅ Inactive users removed (90-day policy)

**PCI-DSS 8.2: Authentication Mechanisms**
- ✅ Multi-factor authentication required (GitHub 2FA)
- ✅ Strong password policy enforced (GitHub requirements)
- ✅ Session management (GitHub handles)

### Evidence Collection

**For Compliance Audits:**

1. **Access Control Matrix:**
   - Document in: `docs/compliance/access-matrix.md`
   - Update: Quarterly
   - Contains: User roles, permissions, justifications

2. **Access Review Logs:**
   - Location: `docs/compliance/access-reviews/`
   - Format: `access-review-YYYY-QQ.md`
   - Retention: 3 years

3. **CODEOWNERS History:**
   - Track via Git history
   - Document rationale for changes
   - Review in quarterly audits

---

## 🔄 Policy Updates

**Last Updated:** February 11, 2026  
**Version:** 1.0  
**Next Review:** May 11, 2026 (Quarterly)

**Changelog:**
- **v1.0 (Feb 2026):** Initial access control policy
  - Extracted from CODEOWNERS file
  - Added detailed procedures
  - Mapped to PCI-DSS requirements

**Review Schedule:**
- **Quarterly:** Policy review and updates
- **Annual:** Comprehensive audit
- **As-needed:** Updates for new threats or requirements

---

## 📝 Related Documents

- **Security Policy:** `SECURITY.md`
- **Code Owners:** `.github/CODEOWNERS`
- **Contributing Guidelines:** `CONTRIBUTING.md`
- **Security Audit Report:** `SECURITY_AUDIT_REPORT.md`
- **Compliance Controls:** `docs/compliance/controls-matrix.md`

---

## ✍️ Approval

**Policy Approved By:**
- Security Team Lead: @RemyLoveLogicAI
- Compliance Officer: TBD
- Repository Owner: @RemyLoveLogicAI

**Effective Date:** February 11, 2026

---

**For questions or policy change requests, contact the security team via the procedures outlined in SECURITY.md**
