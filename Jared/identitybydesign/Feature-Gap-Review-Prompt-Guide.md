# Feature Gap Review Prompt Guide

Use this guide to generate strong prompts in Lovable for identifying product and workflow gaps.

## Objective
Find missing features that block user adoption, retention, or monetization, then prioritize delivery.

## Inputs To Gather Before Prompting
- Target users and top use cases
- Current feature list and known pain points
- Conversion funnel and drop-off points
- Competitor or benchmark products
- Business goals (activation, retention, revenue)
- Team capacity and release cadence

## Master Prompt Template
Copy and fill this template in Lovable:

```text
You are a senior product strategist and UX systems thinker conducting a feature gap review.

Context:
- Product: {{product_name}}
- Target users/personas: {{personas}}
- Core user jobs: {{jobs_to_be_done}}
- Current features: {{current_features}}
- Known pain points: {{pain_points}}
- Funnel data: {{funnel_metrics}}
- Competitor references: {{competitors}}
- Business goals: {{business_goals}}
- Delivery constraints: {{team_constraints}}

Tasks:
1. Identify critical missing capabilities by user journey stage.
2. Flag UX friction and workflow breaks causing drop-off.
3. Compare against competitors for parity and differentiation gaps.
4. Propose features in three buckets:
   - Must-have (launch blockers)
   - Should-have (adoption accelerators)
   - Nice-to-have (strategic differentiators)
5. Provide a 6-week delivery plan with acceptance criteria.
6. Define metrics to validate each shipped feature.

Output format:
- Gap matrix: Journey Stage | Missing Capability | User Impact | Priority
- Prioritized backlog: Feature | Why now | Effort (S/M/L) | Risk if delayed
- 6-week roadmap by sprint
- Feature acceptance criteria (testable)
- KPI tracking plan for each feature
- Assumptions and open questions

Constraints:
- Prioritize user impact and speed-to-value.
- Avoid speculative features without evidence.
- Keep recommendations realistic for a {{team_size}} person team.
```

## Follow-Up Prompt For Execution Readiness
```text
Convert top 5 features into implementation-ready tickets with:
- User story
- Acceptance criteria
- Edge cases
- Dependencies
- Definition of done
```

## Quality Bar (Use As Rubric)
A strong output should:
- Tie features directly to user pain and business goals
- Include measurable success metrics
- Avoid generic feature lists
- Produce sprint-ready, testable outcomes

## Common Gaps To Catch
- Missing onboarding and first-value flow
- Poor account and team management capabilities
- No export/reporting for business users
- Missing notifications and status visibility
- Weak error recovery and support workflows
- No feedback capture loop for product iteration

## Prefilled Prompt (Identity by Design)
Copy and run this directly in Lovable:

```text
You are a senior product strategist and UX systems thinker conducting a feature gap review.

Context:
- Product: Identity by Design
- Target users/personas: Men-focused self-mastery audience (based on public brand language), plus adjacent users not yet validated.
- Core user jobs: Record identity statements in own voice, build repeatable audio installations, reinforce routines with sleep playback over 30 nights.
- Current features: Guided/Freestyle recording, track builder (loops/reverb/frequency/soundscape), clip library (save/name/categorize/edit/delete), player with sleep timer and loop modes, lock-screen playback, installable PWA, promo code beta unlock, referral/share flow.
- Known pain points: No direct user research metrics publicly available; likely trust/privacy concerns for voice data, onboarding drop-off risk, and retention friction for a 30-night behavior program.
- Funnel data: Unknown
- Competitor references: Unknown
- Business goals: Pre-launch growth and activation, stronger habit retention, and conversion to paid tiers (Pro/Elite stated in terms).
- Delivery constraints: Team size unknown, likely lean team based on public positioning and beta/pre-launch indicators.

Tasks:
1. Identify critical missing capabilities by user journey stage.
2. Flag UX friction and workflow breaks causing drop-off.
3. Compare against competitors for parity and differentiation gaps.
4. Propose features in three buckets:
   - Must-have (launch blockers)
   - Should-have (adoption accelerators)
   - Nice-to-have (strategic differentiators)
5. Provide a 6-week delivery plan with acceptance criteria.
6. Define metrics to validate each shipped feature.

Output format:
- Gap matrix: Journey Stage | Missing Capability | User Impact | Priority
- Prioritized backlog: Feature | Why now | Effort (S/M/L) | Risk if delayed
- 6-week roadmap by sprint
- Feature acceptance criteria (testable)
- KPI tracking plan for each feature
- Assumptions and open questions

Constraints:
- Prioritize user impact and speed-to-value.
- Avoid speculative features without evidence.
- Keep recommendations realistic for a small team with unknown final headcount.
```
