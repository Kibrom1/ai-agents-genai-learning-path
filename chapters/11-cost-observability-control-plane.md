# Chapter 11: Cost & Observability / Control Plane Design

*Phase 3 — Agent Architecture Mastery*
## Learn
Request routing by task difficulty, audit logging, and designing a lightweight "control plane" for your own routing/governance policy.

## Resources
- [Inside the LLM Call: GenAI Observability with OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/) — the official OTel post on instrumenting LLM/agent calls
- [Claude models overview](https://docs.claude.com/en/docs/about-claude/models) (pricing reference for building a cost model)

## Exercise
Design a routing policy (which model tier for which task type) with a cost model, and sketch an audit-log schema (an append-only table is a reasonable default).

## Deliverable
A design doc for the control plane's routing policy and cost model.

---
**Phase 3 milestone**: the Chapter 11 design doc, reviewed against real (or realistic sample) traffic patterns.
