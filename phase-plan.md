# Phase Plan

Total span: ~10 weeks core build + ongoing hardening, at roughly 8–10 hrs/week.

## Phase 1 — Foundations Refresh (Week 1)

Fast pass, not a deep-learning course — assumes you already have general engineering chops and just need to fill GenAI-specific gaps.

- LLM fundamentals: tokens, context windows, sampling params, cost/latency tradeoffs across model tiers
- Prompting patterns: system/user/tool roles, few-shot, structured output (JSON mode / tool schemas)
- Embeddings & vector search basics: when RAG actually helps vs. when it's overkill
- **Milestone**: one-page note on which parts of your target use case are prompting problems vs. architecture problems

## Phase 2 — Core GenAI Building Blocks (Weeks 2–4)

- RAG done right: chunking strategy, retrieval evaluation, hybrid search, and when to skip RAG entirely for structured-document extraction
- Tool use & function calling: designing tool schemas an LLM can reliably call
- Agent frameworks survey: pick one to standardize on rather than chasing every new framework
- Structured extraction at scale: confidence scoring, human-in-the-loop review queues, retry/fallback logic
- **Milestone**: a small spike — one real extraction/agent step, working end to end with tool calls + confidence scoring

## Phase 3 — Agent Architecture Mastery (Weeks 5–6)

This is the phase most GenAI tutorials skip, and where most production failures come from.

- Memory & state: short-term (session) vs. long-term (durable) agent memory, and where a durable-execution layer fits
- Multi-agent orchestration: when to split one agent into several specialized agents vs. keeping it monolithic
- Evaluation & guardrails: eval sets for accuracy, hallucination detection, prompt-injection defenses for anything ingesting external content
- Cost & observability: request routing by task difficulty, audit logging, a lightweight "control plane" for your own routing/governance policy
- **Milestone**: design doc for a routing policy (model tier by task type) with a cost model

## Phase 4 — Capstone Project (Weeks 7–9)

Build the **Document Intelligence Agent**: an agent that ingests a document, extracts and validates structured data, cross-references an external data source, and flags anomalies — routed and logged through the control plane you designed in Phase 3.

If you have a second real use case in your own domain, rebuilding the same pattern against it (Chapter 13) is the strongest proof the pattern generalizes rather than being a one-off script.

## Phase 5 — Production Hardening & Review (Week 10)

A structured feedback loop before shipping — here it's a self/peer review against a checklist:

- Security review: prompt injection, data exfiltration via tool calls, PII handling in extracted documents
- Cost audit: actual $/extraction and $/agent-run against the routing model's projections
- Failure-mode review: what happens on low-confidence extraction, model API outage, malformed input
- **Milestone**: go/no-go checklist before the system touches production data

## Format notes

- Weekly cadence with a fixed "build day" block rather than scattered sessions
- Self-paced study + hands-on build time each week, not lecture-only
- Every phase ends in a milestone artifact (doc, spike, or working code) — no phase is "just reading"
- The capstone is real product surface area, not a sandboxed exercise
