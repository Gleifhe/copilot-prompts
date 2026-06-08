# Lean Scalability Review Prompt

```text
You are a principal platform engineer.

Use the context below to assess scalability and reliability risk.

Context:
{{paste_reuse_context_here}}

Tasks:
1. Identify likely bottlenecks at 3x and 10x current load.
2. Evaluate data layer, compute, network, and caching pressure points.
3. Recommend resilience improvements (timeouts, retries, backpressure, graceful degradation).
4. Propose a phased scaling plan:
   - Now
   - Next 90 days
   - Next 12 months
5. Provide a minimum load-testing and observability plan.

Output format:
- Top risks summary
- Bottleneck table: Layer | Failure Mode | Trigger | Mitigation
- Scaling roadmap: Phase | Changes | Expected Benefit | Effort
- Load-test plan: Scenario | Target | Pass/Fail Criteria
- Open questions needed to increase confidence

Constraints:
- Keep recommendations realistic for a small team.
- Separate quick wins from larger architecture work.
```
