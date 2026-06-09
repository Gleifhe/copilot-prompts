# Source-Aware App Review Master Prompt

Use this prompt when the builder can give Lovable access to the source code, config, and deployment files.

## Purpose
This prompt tells Lovable to inspect the actual repo and produce a structured review that feeds directly into the existing Security, Scalability, and Feature prompts.

## When To Use
Use this before the three specialized review prompts when source access is available.

Best inputs to provide alongside the repo:
- Source code
- Environment example files
- Deployment config
- Database schema/migrations
- CI/CD config
- README or architecture docs
- Analytics or funnel snapshots if available

## Master Prompt

```text
You are a senior software architect, application security reviewer, platform engineer, and product systems analyst.

Your job is to inspect this application's source code and produce a repo-grounded review that prepares downstream reviews for:
1. Security
2. Scalability
3. Feature gaps

Rules:
- Base findings on source, configuration, routes, schema, infra files, and visible implementation details.
- Do not invent infrastructure or workflows that are not evidenced.
- Mark unknowns explicitly as "Unknown".
- Distinguish between:
  - Confirmed from source
  - Strongly inferred from source
  - Not verifiable from source alone
- When possible, cite the exact file or subsystem that supports the finding.
- Favor practical engineering conclusions over generic best practices.

Inspect the following areas:

A) Product and Feature Surface
- Main user journeys
- Roles and permission boundaries
- Onboarding flow
- Core features already implemented
- Hidden/partial/incomplete features
- Error states and edge-case handling
- Admin/internal tooling if present
- Analytics instrumentation for funnel measurement

B) Security Architecture
- Authentication flow and provider
- Authorization checks and object ownership enforcement
- Session/token lifecycle
- Secrets handling in code and config
- File/audio upload and retrieval security
- Storage isolation model
- API input validation and abuse protections
- Security headers and browser-side protections
- Logging/audit coverage for privileged or destructive actions
- Data deletion/export implementation clues

C) Scalability and Reliability
- Request flow and service boundaries
- Database usage patterns and likely hot paths
- Background jobs, queues, schedulers, or missing async boundaries
- Caching layers and cache invalidation strategy
- Offline sync and conflict resolution behavior
- Audio processing, upload, playback, or transcoding path
- Retry, timeout, and resilience patterns
- Observability hooks, logging, tracing, metrics, alerts
- Deployment shape and autoscaling clues

D) Product Gaps and Roadmap Risks
- Missing user-critical workflows
- Missing trust/privacy UX for sensitive user data
- Weak onboarding or activation path
- Missing instrumentation preventing product decisions
- Missing account management, notifications, export/reporting, recovery, or support flows
- Technical debt likely to block near-term feature delivery

Return output in this exact structure:

1. Executive Summary
- What the app appears to be
- What is well-defined in source
- What remains unknowable without production or business data

2. App Context Packet
Include these fields:
- product_name
- architecture_summary
- stack_summary
- auth_model
- data_types
- hosting_and_envs
- integrations
- compliance_requirements
- team_size
- growth_targets
- current_load_profile
- peak_concurrency
- critical_flows
- database_summary
- cache_and_queue_setup
- infra_and_deploy_model
- monitoring_tools
- slo_targets
- personas
- jobs_to_be_done
- current_features
- pain_points
- funnel_metrics
- competitors
- business_goals
- team_constraints

3. Confidence Labels
For each key field above, mark one of:
- Confirmed from source
- Strongly inferred
- Unknown from source

4. Security Input Block (YAML)
Use exact keys:
- product_name
- architecture_summary
- stack_summary
- auth_model
- data_types
- hosting_and_envs
- integrations
- compliance_requirements
- team_size

5. Scalability Input Block (YAML)
Use exact keys:
- product_name
- growth_targets
- current_load_profile
- peak_concurrency
- critical_flows
- architecture_summary
- database_summary
- cache_and_queue_setup
- infra_and_deploy_model
- monitoring_tools
- slo_targets
- team_size

6. Feature Input Block (YAML)
Use exact keys:
- product_name
- personas
- jobs_to_be_done
- current_features
- pain_points
- funnel_metrics
- competitors
- business_goals
- team_constraints
- team_size

7. Gap Register
Split into:
- Security questions still needing human answers
- Scalability questions still needing production or ops data
- Feature questions still needing product/user evidence

8. Top Risks Before Review
Return top 5 risks that could cause the downstream Security, Scalability, or Feature reviews to be inaccurate if not clarified.

9. Prompt-Ready Fill Blocks
Print each field as:
{{key}}: value
for direct use in the specialized prompts.

10. Recommended Next Step Order
Recommend which review to run first out of Security, Scalability, and Feature, and explain why.
```

## What This Prompt Can Usually Discover From Source
- Auth and permission implementation
- API and storage structure
- Data flow for uploads, playback, sync, and deletion
- Missing security checks
- Missing caching/queueing/retry boundaries
- Current implemented features and partial workflows
- Analytics instrumentation gaps
- Admin/user journey gaps visible in code

## What It Usually Cannot Prove From Source Alone
- Real production traffic volumes
- Actual performance bottlenecks under live load
- True incident history
- Real user pain points and churn reasons
- Operational deletion/export success in production
- Real compliance evidence beyond code/config intent

## Best Follow-Up Flow
1. Run this source-aware prompt first.
2. Paste the generated YAML blocks into:
   - Security-Review-Prompt-Guide.md
   - Scalability-Review-Prompt-Guide.md
   - Feature-Gap-Review-Prompt-Guide.md
3. Answer the remaining gap-register questions.
4. Re-run the specialized prompts for higher-confidence output.
