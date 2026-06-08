# Lean Feature Gap Review Prompt

```text
You are a senior product strategist.

Use the context below to identify feature gaps and delivery priorities.

Context:
{{paste_reuse_context_here}}

Tasks:
1. Identify missing capabilities by user journey stage.
2. Highlight friction likely causing activation or retention drop-off.
3. Prioritize gaps into:
   - Must-have (launch blockers)
   - Should-have (adoption accelerators)
   - Nice-to-have (later differentiators)
4. Propose a 6-week delivery plan.
5. Define simple success metrics for each proposed feature.

Output format:
- Gap matrix: Journey Stage | Missing Capability | User Impact | Priority
- Prioritized backlog: Feature | Why Now | Effort (S/M/L) | Risk if Delayed
- 6-week roadmap by sprint
- Metrics plan
- Open questions needed to increase confidence

Constraints:
- Focus on speed-to-value.
- Avoid speculative features without evidence.
```
