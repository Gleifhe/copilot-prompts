# App Information Gathering Prompt

Use this prompt in Lovable first, before running security, scalability, and feature-gap reviews.

## Purpose
Collect a structured, complete context packet about the app so later review prompts produce specific and actionable recommendations.

## How To Use
1. Copy the prompt below into Lovable.
2. Provide all known app details.
3. If details are unknown, explicitly return "Unknown" rather than guessing.
4. Save the result as your "App Context Packet".
5. Copy the generated handoff blocks directly into the Security, Scalability, and Feature review prompts.

## Placeholder Contract (Used By The Other 3 Files)

Use these exact placeholder names so outputs plug in with no renaming.

Common placeholders:
- product_name
- architecture_summary
- team_size

Security placeholders:
- stack_summary
- auth_model
- data_types
- hosting_and_envs
- integrations
- compliance_requirements

Scalability placeholders:
- growth_targets
- current_load_profile
- peak_concurrency
- critical_flows
- database_summary
- cache_and_queue_setup
- infra_and_deploy_model
- monitoring_tools
- slo_targets

Feature placeholders:
- personas
- jobs_to_be_done
- current_features
- pain_points
- funnel_metrics
- competitors
- business_goals
- team_constraints

## Master Information-Gathering Prompt

```text
You are a senior solutions architect and product analyst.
Your task is to gather complete project context for an application review focused on security, scalability, and feature-gap analysis.

Important rules:
- Do not assume missing facts.
- Ask follow-up questions where information is missing.
- Mark unknown items explicitly as "Unknown".
- Keep output concise but complete.

Collect and return the following sections:

1) Product and Business Context
- App name
- One-line value proposition
- Target users/personas
- Core jobs-to-be-done
- Business model (if any)
- Stage: prototype/beta/production
- Timeline and launch goals
- Team size and skill mix
- Delivery constraints (time, budget, compliance)

2) Functional Scope
- Current core features
- Admin capabilities
- User roles and permissions model
- Planned features in next 3 months
- Known user complaints or friction points
- Critical workflows that must not fail

3) Technical Architecture
- Frontend stack and hosting
- Backend stack and hosting
- Database(s) and storage systems
- APIs (internal/external)
- Third-party integrations and dependencies
- Background jobs, queues, schedulers
- Caching strategy
- Search/indexing components
- File upload/processing flows

4) Security and Privacy Context
- Authentication method(s)
- Authorization model (RBAC/ABAC/custom)
- Sensitive data types handled
- Data encryption in transit and at rest
- Secrets management approach
- Session management approach
- Rate limiting and abuse protection
- Audit logs and incident response process
- Compliance requirements (GDPR, SOC2, HIPAA, PCI, etc.)

5) Scalability and Reliability Context
- Current DAU/MAU
- Peak concurrent users now
- Projected growth (3/6/12 months)
- Request volume profile (read/write mix)
- SLO/SLA targets (latency, uptime, error budget)
- Current bottlenecks and outages experienced
- Autoscaling strategy
- Database scaling strategy
- Failover/disaster recovery posture
- Monitoring, metrics, tracing, alerting stack

6) Delivery and Quality Process
- Repo and branching strategy
- CI/CD pipeline and deployment frequency
- Test coverage by layer (unit/integration/e2e)
- Security testing in pipeline
- Release rollback process
- Environments (dev/stage/prod) parity quality

7) Evidence and Unknowns
- Known facts with confidence level (High/Medium/Low)
- Unknown or unverified items
- Top 10 clarification questions needed before final review

Output format:
A) "App Context Packet" in structured markdown
B) "Data Quality Score" from 0-100 with rationale
C) "Readiness for Review" as: Ready / Partially Ready / Not Ready
D) "Next Questions" prioritized list (highest impact first)

After producing the packet, provide ALL of the following plug-in outputs:

E) "Security Prompt Input Block" in YAML using these exact keys:
product_name, architecture_summary, stack_summary, auth_model, data_types,
hosting_and_envs, integrations, compliance_requirements, team_size

F) "Scalability Prompt Input Block" in YAML using these exact keys:
product_name, growth_targets, current_load_profile, peak_concurrency,
critical_flows, architecture_summary, database_summary, cache_and_queue_setup,
infra_and_deploy_model, monitoring_tools, slo_targets, team_size

G) "Feature Prompt Input Block" in YAML using these exact keys:
product_name, personas, jobs_to_be_done, current_features, pain_points,
funnel_metrics, competitors, business_goals, team_constraints, team_size

H) "Prompt-Ready Fill Blocks" where each key is printed as:
{{key}}: value
for direct copy/paste into each downstream prompt template.

I) "JSON Mirror" with three objects named:
security_input, scalability_input, feature_input
that contain the same fields as E/F/G.

J) "Unmapped Fields" list for any data that did not fit placeholders.
```

## Optional Follow-Up Prompt (Gap Closure)

```text
Using your previous App Context Packet, generate a gap-closure interview checklist.
Prioritize the top missing data points that would most improve:
1) security analysis quality,
2) scalability analysis quality,
3) feature-gap analysis quality.

Return:
- 15 interview questions max
- Why each question matters
- Which review area it unlocks
- Suggested owner (engineering, product, security, ops)
```

## Output Acceptance Criteria
A good result should:
- Distinguish facts from assumptions
- Surface unknowns clearly
- Include enough architecture and operational detail to support concrete recommendations
- Produce reusable handoff blocks for all three downstream prompts
- Use exact placeholder names from the contract above
- Include YAML and JSON forms so data can be reused in different workflows
