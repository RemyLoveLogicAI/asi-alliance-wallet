# Access Control Policy
## ASI Alliance Wallet Repository

**Version:** 1.0  
**Last Updated:** February 11, 2026  
**Policy Owner:** Security Team Lead  
**Review Schedule:** Quarterly

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [Emergency Contacts](#emergency-contacts)
3. [Escalation Procedures](#escalation-procedures)
4. [Access Control Requirements](#access-control-requirements)
5. [Review Requirements](#review-requirements)
6. [Protection Rules](#protection-rules)
7. [Least Privilege Principle](#least-privilege-principle)
8. [Access Review Process](#access-review-process)
9. [Compliance Mapping](#compliance-mapping)

---

## 🔒 Overview

This document defines the access control policy for the ASI Alliance Wallet repository, implementing PCI-DSS requirements 7.1 (Access Control) and 7.2 (Least Privilege).

The CODEOWNERS file in `.github/CODEOWNERS` enforces these policies through automated review requests.

---

## 📞 Emergency Contacts

### Security Emergencies

**Primary Contact:** Security Team Lead  
**GitHub:** @RemyLoveLogicAI  
**Email:** security@fetch.ai  
**Emergency:** PagerDuty (authorized personnel only)

**Secondary Contact:**  
**GitHub:** @agent-dominatrix  
**Role:** Security Operations

### General Questions

**Technical Lead:** @sh-wallet  
**Backend Lead:** @AbbasAliLokhandwala  
**Community:** Discord/Telegram channels

### Compliance & Legal

**Compliance Officer:** compliance@fetch.ai  
**Privacy/GDPR:** privacy@fetch.ai  
**Legal:** legal@fetch.ai

---

## 🚨 Escalation Procedures

### Escalation Path

**Level 1: GitHub PR Review Request**
- CODEOWNERS automatically request reviews
- Owners notified via GitHub notifications
- Expected response: Within 1 business day

**Level 2: Direct Mention in PR Comments**
- Tag specific owners: `@owner-username`
- Use for urgent reviews
- Expected response: Within 4 hours

**Level 3: Direct Email to Team**
- Email security@fetch.ai or technical leads
- Use for time-sensitive issues
- Expected response: Within 2 hours

**Level 4: PagerDuty (CRITICAL ONLY)**
- For production incidents only
- Security breaches
- System outages
- Expected response: Within 15 minutes

### When to Escalate

**Immediate Escalation (Level 4):**
- Security breach detected
- Private key exposure
- Production system down
- Active attack in progress

**Urgent (Level 3):**
- Critical security vulnerability
- Blocking production deployment
- Compliance deadline imminent

**Standard (Level 1-2):**
- Regular code reviews
- Non-critical security fixes
- Documentation updates
- Routine dependency updates

---

## 🔐 Access Control Requirements

### Repository Access Levels

**Read Access:**
- All contributors
- External auditors (time-limited)
- Automated tools (approved bots only)

**Write Access:**
- Core team members only
- Requires 2FA enabled
- Regular access review (quarterly)
- Immediate revocation upon leaving team

**Admin Access:**
- Repository owner only (@RemyLoveLogicAI)
- Security team lead
- Emergency access only
- All actions logged and audited

**Security Admin:**
- Security team lead
- Manages security policies
- Reviews security-critical changes
- Conducts security audits

---

## ✅ Review Requirements

### Standard Pull Requests

**Minimum Requirements:**
- At least 1 approval from CODEOWNERS
- All CI checks must pass
- No merge conflicts
- Branch up-to-date with base branch

### Security-Critical Changes

**Enhanced Requirements:**
- **2 approvals** from security team members
- Security team review mandatory
- Security impact assessment completed
- All security tests passing
- Documentation updated

**Security-Critical Paths:**
- `packages/crypto/**`
- `packages/background/src/keyring/**`
- `packages/**/encryption/**`
- `packages/background/src/auth/**`
- `packages/background/src/tx/**`
- `SECURITY.md`
- `.github/dependabot.yml`
- `.github/workflows/security*.yml`

### Dependency Changes

**Requirements:**
- Security team review required
- Dependency verification completed
- npm audit clean (no critical/high)
- Signatures verified
- Lock files updated

### Breaking Changes

**Requirements:**
- All maintainer approval required
- Migration guide provided
- Deprecation timeline documented
- Changelog updated
- Community notification prepared

---

## 🛡️ Protection Rules

### Main Branch Protection

**Required Settings:**
- Require pull request reviews before merging
- Require at least 2 approving reviews
- Dismiss stale pull request approvals when new commits are pushed
- Require review from CODEOWNERS
- Require status checks to pass before merging
- Require branches to be up to date before merging
- Require signed commits
- Include administrators (no bypass)

**Status Checks Required:**
- Continuous Integration (CI)
- Security scanning
- Unit tests
- Integration tests
- License compliance

### Release Branch Protection

**Additional Requirements:**
- All main branch protections
- Signed commits mandatory
- Linear history enforced
- No force pushes
- No deletions

### Security Branch Protection

**Restricted Access:**
- Security team only
- Separate branch for security fixes
- Not publicly visible until patched
- Enhanced monitoring

---

## 👥 Least Privilege Principle

### Access Grant Criteria

**Read Access:**
- Granted to: Contributors, community members
- Purpose: Code review, issue reporting
- Duration: Indefinite (with activity)
- Review: Annually

**Write Access:**
- Granted to: Core team members
- Purpose: Code contributions, PR management
- Duration: While actively contributing
- Review: Quarterly
- Requires: 2FA, signed commits, code of conduct agreement

**Admin Access:**
- Granted to: Repository owner, security lead
- Purpose: Security management, emergency response
- Duration: Role-based
- Review: Monthly
- Requires: Enhanced security training, incident response training

### Access Limitations

**Branch Restrictions:**
- Main branch: No direct commits
- Release branches: Release team only
- Security branches: Security team only
- Feature branches: Creator + reviewers

**Action Restrictions:**
- Force push: Disabled on protected branches
- Delete: Disabled on protected branches
- Bypass reviews: Disabled for all users
- Settings changes: Admin only

---

## 🔄 Access Review Process

### Quarterly Access Review

**Review Schedule:**
- Q1 Review: February 15
- Q2 Review: May 15
- Q3 Review: August 15
- Q4 Review: November 15

**Review Procedure:**

1. **Generate Access Report**
   ```bash
   # List all collaborators
   gh api repos/RemyLoveLogicAI/asi-alliance-wallet/collaborators
   
   # Check last activity
   gh api repos/RemyLoveLogicAI/asi-alliance-wallet/stats/contributors
   ```

2. **Review Each User**
   - Verify still requires access
   - Check activity level (commits, reviews)
   - Confirm role is still current
   - Validate 2FA enabled

3. **Take Action**
   - Remove: Inactive users (90+ days)
   - Downgrade: Users with reduced role
   - Maintain: Active contributors
   - Upgrade: Users requiring elevated access

4. **Document**
   - Log all access changes
   - Update access matrix
   - Notify affected users
   - Archive report for compliance

### Immediate Revocation

**Automatic Revocation Triggers:**
- User leaves organization
- Security incident involving user account
- Policy violation
- Inactivity >90 days
- 2FA disabled
- Compliance requirement

**Revocation Procedure:**
```bash
# Remove collaborator immediately
gh api repos/RemyLoveLogicAI/asi-alliance-wallet/collaborators/USERNAME \
  -X DELETE

# Revoke all tokens
# Audit recent activity
# Notify security team
# Document in audit log
```

### Emergency Access

**Break-Glass Procedure:**

1. **Request:** Security incident requires immediate access
2. **Approval:** Security team lead or CTO
3. **Grant:** Temporary admin access (time-limited)
4. **Monitor:** All actions logged
5. **Revoke:** Automatic after incident resolution
6. **Audit:** Post-incident review of all actions

---

## 📋 Compliance Mapping

### PCI-DSS Requirements

**Requirement 7.1: Access Control**
- Implementation: CODEOWNERS file + branch protection
- Evidence: This policy + GitHub audit logs
- Testing: Quarterly access reviews
- Responsible: Security Team Lead

**Requirement 7.2: Least Privilege**
- Implementation: Role-based access grants
- Evidence: Access matrix + approval logs
- Testing: Monthly access audits
- Responsible: Repository Owner

**Requirement 8.1: User Identification**
- Implementation: GitHub authentication
- Evidence: Commit signatures, audit logs
- Testing: Signature verification
- Responsible: All users

**Requirement 8.2: Authentication**
- Implementation: 2FA mandatory for write access
- Evidence: GitHub security settings
- Testing: Automated enforcement
- Responsible: Platform (GitHub)

### Audit Evidence

**Maintained Documents:**
- Access grant approvals
- Quarterly access review reports
- Access revocation logs
- Emergency access logs
- Training completion records

**Retention Period:** 3 years (compliance requirement)

**Storage Location:** `docs/compliance/access-reviews/`

---

## 📊 Access Matrix

### Current Repository Roles

| User/Team | Role | Access Level | 2FA | Last Review |
|-----------|------|--------------|-----|-------------|
| @RemyLoveLogicAI | Owner | Admin | ✅ | 2026-02-11 |
| @agent-dominatrix | Security Lead | Write + Security | ✅ | 2026-02-11 |
| @sh-wallet | Technical Lead | Write | ✅ | 2026-02-11 |
| @AbbasAliLokhandwala | Backend Lead | Write | ✅ | 2026-02-11 |

**Next Review:** 2026-05-15

---

## 🔄 Policy Maintenance

### Review Schedule

- **Quarterly:** Full policy review
- **Monthly:** Access review
- **Weekly:** Activity monitoring
- **Daily:** Anomaly detection

### Update Procedure

1. Propose changes via pull request
2. Security team review
3. Compliance officer approval
4. Update effective date
5. Notify all team members
6. Archive previous version

### Version History

- **v1.0 (2026-02-11):** Initial policy (extracted from CODEOWNERS)
- Previous: Embedded in CODEOWNERS file

---

## ✅ Acknowledgment

All team members with write access must acknowledge understanding of this policy.

**To acknowledge:**
1. Read this policy completely
2. Complete security training
3. Enable 2FA on GitHub account
4. Sign Code of Conduct
5. Comment on internal tracking issue

---

## 📚 Related Documentation

- **SECURITY.md:** Security policy and incident response
- **CONTRIBUTING.md:** Contribution guidelines
- **CODE_OF_CONDUCT.md:** Community standards
- **.github/CODEOWNERS:** Automated ownership enforcement
- **docs/compliance/:** Compliance documentation

---

## 📝 Questions or Updates?

For questions about this policy:
- **Email:** security@fetch.ai
- **GitHub:** Open issue with `governance` label
- **Slack:** #security-team channel

To propose policy updates:
- Submit pull request to this file
- Request security team review
- Include rationale for changes
- Update version and last updated date

---

*This policy is effective immediately and supersedes all previous informal access control procedures.*
