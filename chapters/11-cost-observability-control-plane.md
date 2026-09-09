# Chapter 11: Cost & Observability / Control Plane Design

*Phase 3 — Agent Architecture Mastery*
## What you need to know

**Route by task difficulty, not uniformly.** Not every call in an agent pipeline needs your most capable (and expensive) model. A classification or routing step is often well-served by a small/fast model; a complex reasoning or generation step may genuinely need the largest tier. A "control plane" in the simplest sense is just a routing policy: given a task type (and optionally a difficulty signal), which model tier handles it, with what fallback if that tier fails or times out.

**Audit logging is what makes routing decisions debuggable and compliant.** Every LLM call worth tracking should log: which model was called, why (the routing decision), the token counts, the latency, and — for anything touching sensitive data — enough context to reconstruct what happened without storing the full raw content unnecessarily. An append-only log table is a reasonable, simple default; you don't need a specialized observability platform to start.

**Cost modeling needs real numbers, not vibes.** Before you can optimize routing, you need per-task-type baseline costs: tokens in, tokens out, model tier, and how often each task type actually runs. Multiply that out and you have a real cost projection you can validate later (Chapter 15) rather than an assumption.

**Standardize your instrumentation early.** Whatever you use to trace/log LLM and agent calls, do it consistently across every call site from the start — retrofitting observability onto a system that's already grown organically is far more painful than building it in from the first agent you ship. The OpenTelemetry GenAI semantic conventions are a reasonable standard to align with if you want your logging to interoperate with off-the-shelf observability tooling later.

## Exercise

1. List the distinct task types in your target agent system (e.g. classification, extraction, validation, generation) and assign each a model tier based on how much reasoning it actually needs.
2. Estimate a cost-per-task-type using real token counts from earlier chapters' exercises, and roll that up into a rough monthly cost projection at your expected volume.
3. Sketch an audit-log schema: what fields does every logged call need (model, task type, tokens, latency, routing decision, timestamp, and a way to trace a call back to the record/request it served)?

## Deliverable

A design doc: the routing policy (task type → model tier → fallback), the cost model, and the audit-log schema.

---
**Phase 3 milestone**: this design doc, reviewed against real (or realistic sample) traffic patterns.

## Insurance Claims Example
Design a routing policy by claims task type: routine property-damage estimate extraction to a small/fast tier, complex bodily-injury narrative summarization or liability assessment to a larger tier. The audit log matters doubly here — claims handling is a regulated process, so your append-only log of which model made or influenced which determination, with what confidence, isn't just cost tracking, it's the record you'd need to produce for a compliance or dispute review.


## Resources
- [Inside the LLM Call: GenAI Observability with OpenTelemetry](https://opentelemetry.io/blog/2026/genai-observability/) — the official OTel post on instrumenting LLM/agent calls
- [Claude models overview](https://docs.claude.com/en/docs/about-claude/models) (pricing reference for building a cost model)
