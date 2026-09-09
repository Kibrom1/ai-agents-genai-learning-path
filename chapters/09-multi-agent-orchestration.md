# Chapter 9: Multi-Agent Orchestration

*Phase 3 — Agent Architecture Mastery*
## What you need to know

**Split agents along a real boundary, not an arbitrary one.** The right reason to split one agent into two is that they need different context, different tools, or different failure handling — not just "this feels like a lot for one agent." A extraction agent and a validation agent are a natural split: the validator needs the extracted output and a different set of checks/tools, and its failure mode (flag for review) is different from the extractor's (retry or fallback).

**The handoff contract is the interface.** When one agent's output becomes another's input, define that boundary as an explicit schema — not "pass along whatever text the first agent produced." This is exactly the structured-output discipline from Chapter 2, applied at the agent-to-agent boundary instead of the agent-to-caller boundary. A loose handoff (unstructured text) is where multi-agent systems become undebuggable, because errors surface far from their cause.

**Failure containment: one agent's failure shouldn't silently corrupt the next.** If the extraction agent fails or returns low confidence, the validation agent needs to know that explicitly (via the handoff schema) rather than receiving a plausible-looking but wrong result and validating it as if it were solid. Build "did the upstream step actually succeed" into the contract, not just the happy-path fields.

**Orchestrator-worker is the most common useful pattern.** One agent (or plain code) plans/routes work, and specialized worker agents execute narrow subtasks and report back. This scales better than a single agent trying to do everything, and it keeps each worker's prompt and tools focused enough to reason about and test independently.

## Exercise

1. Split your Chapter 7 extraction agent into two: an extraction agent and a separate validation agent that reviews its output.
2. Define the handoff schema between them explicitly, including a field that communicates upstream confidence/success — not just the extracted data.
3. Test the failure path: feed the validator a deliberately low-confidence or malformed extraction result and confirm it handles that case explicitly rather than treating it as valid input.

## Deliverable

A two-agent pipeline with a clear, documented handoff contract (schema) between them.

## Resources
- [Building Effective AI Agents — Anthropic](https://www.anthropic.com/engineering/building-effective-agents) (re-read the orchestrator-worker section specifically)
- [Workflows and agents — LangGraph Docs](https://docs.langchain.com/oss/python/langgraph/workflows-agents) (multi-agent graph patterns)
