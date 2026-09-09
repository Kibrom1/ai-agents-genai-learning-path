# Chapter 8: Agent Memory & State

*Phase 3 — Agent Architecture Mastery*
## Learn
Short-term (session) vs. long-term (durable) memory, and where a durable-execution layer fits as the state/retry layer for long-running agent workflows.

## Resources
- [Inngest Docs](https://www.inngest.com/docs) — a good default if you want durable execution without standing up your own infra (Temporal and Restate are viable alternatives)
- [The Principles of Durable Execution](https://www.inngest.com/blog/principles-of-durable-execution)
- [Reliably run critical workflows](https://www.inngest.com/docs/patterns/durable/reliably-run-critical-workflows)

## Exercise
Model a multi-step agent workflow (extract → validate → enrich) as durable functions/steps with proper retry and idempotency.

## Deliverable
A workflow diagram plus working step functions.
