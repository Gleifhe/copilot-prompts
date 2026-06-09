# Scalability Review Prompt Guide

Use this guide to generate strong prompts in Lovable for scalability and performance readiness.

## Objective
Find bottlenecks early, define scaling milestones, and reduce failure risk as traffic grows.

## Inputs To Gather Before Prompting
- Current and projected active users
- Peak concurrency assumptions
- Critical user journeys and SLAs
- Current architecture and data flow
- Database schema hotspots and read/write mix
- Caching, queueing, and background job setup
- Hosting and autoscaling capabilities
- Observability stack (metrics, tracing, logs)

## Master Prompt Template
Copy and fill this template in Lovable:

```text
You are a principal platform engineer conducting a scalability review for a production-bound app.

Context:
- Product: {{product_name}}
- User growth target: {{growth_targets}}
- Current load: {{current_load_profile}}
- Peak profile: {{peak_concurrency}}
- Critical flows: {{critical_flows}}
- Stack/architecture: {{architecture_summary}}
- Data layer: {{database_summary}}
- Caching/queues: {{cache_and_queue_setup}}
- Infrastructure: {{infra_and_deploy_model}}
- Observability: {{monitoring_tools}}
- Performance goals: {{slo_targets}}

Tasks:
1. Identify top bottlenecks likely at 3x, 10x, and 30x load.
2. Analyze compute, DB, cache, and network pressure points.
3. Recommend scaling approach for each layer (horizontal/vertical/caching/sharding/etc.).
4. Propose resilience improvements (timeouts, retries, circuit breakers, backpressure).
5. Design a phased roadmap:
   - Now (pre-scale)
   - Next 90 days
   - Next 12 months
6. Define load testing plan with scenario matrix and pass/fail criteria.
7. Provide observability requirements and alert thresholds.

Output format:
- Top risks summary (ordered by impact)
- Bottleneck table: Layer | Failure Mode | Trigger | Mitigation
- Scaling roadmap: Phase | Changes | Expected benefit | Effort
- Load-test plan: Scenario | Target RPS/users | SLO | Exit criteria
- Capacity assumptions and unknowns

Constraints:
- Recommend pragmatic steps for a {{team_size}} person team.
- Separate quick wins from architectural investments.
- Tie each recommendation to measurable outcomes.
```

## Follow-Up Prompt For Capacity Planning
```text
Convert your recommendations into a capacity planning sheet with:
- Baseline assumptions
- Capacity model equations
- Resource thresholds for scaling triggers
- Monthly review cadence and owner roles
```

## Quality Bar (Use As Rubric)
A strong output should:
- Quantify breakpoints (not only say "might be slow")
- Include concrete SLO-linked recommendations
- Distinguish immediate fixes from long-term architecture work
- Include testable acceptance criteria

## Common Gaps To Catch
- DB connection pool exhaustion
- Missing async offload for heavy workflows
- No cache invalidation strategy
- N+1 query patterns in critical endpoints
- No regional strategy for geographically distributed users
- Weak degradation behavior under partial outages

## Prefilled Prompt (Identity by Design)
Copy and run this directly in Lovable:

```text
You are a principal platform engineer conducting a scalability review for a production-bound app.

Context:
- Product: Identity by Design
- User growth target: Unknown (pre-launch/beta signals present)
- Current load: Unknown
- Peak profile: Unknown
- Critical flows: sign-in/account access, voice recording capture, save to library, clip retrieval, track assembly/playback, sleep timer playback, cross-session sync.
- Stack/architecture: PWA SPA with service worker registration and offline/local caching behavior. Served via Cloudflare.
- Data layer: Not publicly confirmed. Likely metadata persistence for users, clips, categories, mixes, and playback settings.
- Caching/queues: Browser local storage and IndexedDB are explicitly referenced in policy. Backend queue/transcoding architecture unknown.
- Infrastructure: Cloudflare-fronted web app at identitybydesign.app. Backend deployment and region strategy unknown.
- Observability: Public signal of analytics endpoint proxy (/~api/analytics). Full metrics/tracing/logging stack unknown.
- Performance goals: Unknown

Tasks:
1. Identify top bottlenecks likely at 3x, 10x, and 30x load.
2. Analyze compute, DB, cache, and network pressure points.
3. Recommend scaling approach for each layer (horizontal/vertical/caching/sharding/etc.).
4. Propose resilience improvements (timeouts, retries, circuit breakers, backpressure).
5. Design a phased roadmap:
   - Now (pre-scale)
   - Next 90 days
   - Next 12 months
6. Define load testing plan with scenario matrix and pass/fail criteria.
7. Provide observability requirements and alert thresholds.

Output format:
- Top risks summary (ordered by impact)
- Bottleneck table: Layer | Failure Mode | Trigger | Mitigation
- Scaling roadmap: Phase | Changes | Expected benefit | Effort
- Load-test plan: Scenario | Target RPS/users | SLO | Exit criteria
- Capacity assumptions and unknowns

Constraints:
- Recommend pragmatic steps for a small team with unknown final headcount.
- Separate quick wins from architectural investments.
- Tie each recommendation to measurable outcomes.
```
