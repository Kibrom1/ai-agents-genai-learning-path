# Chapter 15: Cost Audit

*Phase 5 — Production Hardening & Review*
## What you need to know

**Projections drift from reality for predictable reasons**: retries you didn't account for, a task type that turned out more complex than expected (routed to a bigger model more often than planned), or prompt/context growth over time (few-shot examples and system prompts tend to accumulate). A cost audit isn't just "were we right" — it's diagnosing *which* of these caused the gap.

**Measure at the task-type level, not just in aggregate.** An aggregate "total spend was 20% over projection" tells you nothing actionable. Break it down by the task types you defined in Chapter 11 — one task type running 3x over budget while others are on target is a very different problem than uniform overrun.

## Do

Pull real usage data from your Chapter 11 audit logs (or provider dashboard) and compare actual $/extraction and $/agent-run against the Chapter 11 cost model, broken down by task type.

## Deliverable

A cost audit doc: projected vs. actual, broken down by task type, with a note on any routing-policy adjustment this suggests.

## Resources
- [Claude models overview](https://docs.claude.com/en/docs/about-claude/models) (pricing)
- Your Chapter 11 observability setup, to pull real numbers
