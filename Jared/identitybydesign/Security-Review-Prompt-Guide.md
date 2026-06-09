# Security Review Prompt Guide

Use this guide to generate strong prompts in Lovable for application security reviews.

## Objective
Identify real security risks, prioritize fixes, and define practical mitigation steps for a small team.

## Inputs To Gather Before Prompting
- App summary and user roles
- Tech stack (frontend, backend, DB, cloud)
- Auth method (OAuth, email/password, SSO)
- Sensitive data types (PII, payment, health, secrets)
- Existing controls (WAF, MFA, rate limits, encryption)
- Compliance scope (GDPR, SOC2, HIPAA, PCI, none)
- Public endpoints and integration points

## Master Prompt Template
Copy and fill this template in Lovable:

```text
You are a senior application security architect performing a practical, developer-friendly security review.

Context:
- Product: {{product_name}}
- Architecture: {{architecture_summary}}
- Stack: {{stack_summary}}
- AuthN/AuthZ: {{auth_model}}
- Data sensitivity: {{data_types}}
- Deployment: {{hosting_and_envs}}
- Integrations: {{integrations}}
- Compliance target: {{compliance_requirements}}

Tasks:
1. Produce a threat model using STRIDE-style categories.
2. Identify top vulnerabilities by severity (Critical/High/Medium/Low).
3. List likely attack paths and prerequisite conditions.
4. Evaluate auth, authorization, session handling, and secrets management.
5. Evaluate data protection in transit and at rest.
6. Evaluate API abuse resistance (rate limits, anti-automation, abuse controls).
7. Provide a prioritized remediation plan for:
   - 48 hours
   - 2 weeks
   - 1 quarter
8. Include verification checks and test cases for each remediation.

Output format:
- Executive summary (max 10 lines)
- Risk table: Risk | Severity | Affected Area | Exploitability | Business Impact
- Remediation backlog: Item | Priority | Effort (S/M/L) | Owner Type
- Security test checklist for CI/CD
- Open questions and assumptions

Constraints:
- Keep recommendations realistic for a {{team_size}} person team.
- Prefer high-impact, low-effort fixes first.
- Avoid generic advice; tie each recommendation to the provided architecture.
```

## Follow-Up Prompt For Deeper Findings
```text
Take the top 3 risks from your previous output and expand each into:
- Root cause
- Exact failure scenario
- Concrete fix options (quick fix vs robust fix)
- Regression test cases
- Monitoring alert conditions
```

## Quality Bar (Use As Rubric)
A strong output should:
- Reference your actual architecture details
- Prioritize by exploitability and impact
- Include implementation-ready steps, not only concepts
- Include verification/testing guidance

## Common Gaps To Catch
- Broken object-level authorization (BOLA)
- Overly broad API keys and leaked secrets
- Missing audit logging for privileged actions
- Insecure file upload handling
- Weak password reset or session invalidation
- Unbounded retries and no abuse controls

## Prefilled Prompt (Identity by Design)
Copy and run this directly in Lovable:

```text
You are a senior application security architect performing a practical, developer-friendly security review.

Context:
- Product: Identity by Design
- Architecture: Publicly visible as a single-page progressive web app with service worker and offline-capable storage patterns. Frontend appears bundled and served behind Cloudflare. App handles user-created voice recordings with cloud sync.
- Stack: Frontend SPA plus PWA (manifest/service worker). CDN/edge via Cloudflare. Potential backend/auth/storage integrations are hinted in client bundle strings (including Supabase-like auth/storage patterns), but are not fully verified.
- AuthN/AuthZ: Account-based authentication is implied by privacy and terms language and user-scoped storage references. Exact auth provider and token/session design are not publicly confirmed.
- Data sensitivity: Name, email, voice recordings, usage analytics events, referral/campaign parameters, and anonymized aggregated transcription-derived themes.
- Deployment: Public app hosted on identitybydesign.app behind Cloudflare edge. Environment model (dev/stage/prod) not publicly disclosed.
- Integrations: Cloudflare, cloud object storage signals, analytics endpoint proxied via /~api/analytics, PWA service worker and offline cache behavior.
- Compliance target: Privacy policy references GDPR and CCPA rights; app is 18+; app disclaimers state not medical or psychological care.

Tasks:
1. Produce a threat model using STRIDE-style categories.
2. Identify top vulnerabilities by severity (Critical/High/Medium/Low).
3. List likely attack paths and prerequisite conditions.
4. Evaluate auth, authorization, session handling, and secrets management.
5. Evaluate data protection in transit and at rest.
6. Evaluate API abuse resistance (rate limits, anti-automation, abuse controls).
7. Provide a prioritized remediation plan for:
   - 48 hours
   - 2 weeks
   - 1 quarter
8. Include verification checks and test cases for each remediation.

Output format:
- Executive summary (max 10 lines)
- Risk table: Risk | Severity | Affected Area | Exploitability | Business Impact
- Remediation backlog: Item | Priority | Effort (S/M/L) | Owner Type
- Security test checklist for CI/CD
- Open questions and assumptions

Constraints:
- Keep recommendations realistic for a small team with unknown final headcount.
- Prefer high-impact, low-effort fixes first.
- Avoid generic advice; tie each recommendation to the provided architecture.
```
