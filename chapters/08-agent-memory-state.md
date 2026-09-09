# Chapter 8: Agent Memory & State

*Phase 3 — Agent Architecture Mastery*
## What you need to know

**Short-term vs. long-term memory are different problems.** Short-term (session) memory is just the conversation/tool-call history within one request — it lives and dies with the request and is bounded by the context window. Long-term (durable) memory is state that survives across requests, retries, and process restarts — an agent's progress through a multi-step workflow, or facts it should remember between sessions. Conflating the two is a common source of bugs: don't build a custom database for something that's really just conversation history, and don't rely on in-memory state for something that needs to survive a crash.

**Durable execution solves the "what if this crashes halfway through" problem.** A multi-step agent workflow (extract → validate → enrich) run as a plain function fails entirely if step 3 of 5 crashes — you lose steps 1 and 2's work and have no record of where it stopped. A durable-execution framework checkpoints each step's result, so a crash resumes from the last completed step rather than starting over, and gives you built-in retry/idempotency per step instead of hand-rolled retry logic scattered through your code.

**Idempotency is what makes retries safe.** If step 2 of your workflow "creates a database record" and it's retried after a partial failure, does it create a duplicate? Durable-execution frameworks handle this by tracking which steps already completed, but only if you design each step to be safely re-runnable (or explicitly guarded) — this is a design discipline, not something the framework gives you for free.

## Exercise

1. Model a multi-step agent workflow (extract → validate → enrich, or an equivalent 3-step pipeline from your own use case) using a durable-execution framework.
2. Implement each step with explicit retry behavior.
3. Deliberately kill the process mid-workflow (after step 1 or 2 completes) and confirm it resumes from the correct point rather than restarting from scratch.
4. Verify that retrying a step doesn't produce duplicate side effects (e.g. a duplicate database write).

## Deliverable

A workflow diagram plus working step functions, with a note confirming the crash-resume behavior actually works as expected.

## Insurance Claims Example
A claim's lifecycle is inherently long-running — FNOL to closing can span days to months, with waits for documents, adjuster availability, and third-party responses. This is exactly what durable execution is for: model the claim as a durable workflow (FNOL received → coverage verified → assigned to adjuster → documents requested → investigation complete → reserve set → settlement offered → closed), where each stage is a checkpointed step. Kill the process mid-workflow (e.g. right after "documents requested") and confirm it resumes waiting for documents rather than restarting the claim from FNOL.


## Resources
- [Inngest Docs](https://www.inngest.com/docs) — a good default if you want durable execution without standing up your own infra (Temporal and Restate are viable alternatives)
- [The Principles of Durable Execution](https://www.inngest.com/blog/principles-of-durable-execution)
- [Reliably run critical workflows](https://www.inngest.com/docs/patterns/durable/reliably-run-critical-workflows)
