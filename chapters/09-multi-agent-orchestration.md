# Chapter 9: Multi-Agent Orchestration

*Phase 3 — Agent Architecture Mastery*
## Learn
When to split one agent into several specialized agents (e.g. extraction agent → validation agent → enrichment agent) vs. keeping it monolithic, and handoff/failure-containment patterns between agents.

## Resources
- [Building Effective AI Agents — Anthropic](https://www.anthropic.com/engineering/building-effective-agents) (re-read the orchestrator-worker section specifically)
- [Workflows and agents — LangGraph Docs](https://docs.langchain.com/oss/python/langgraph/workflows-agents) (multi-agent graph patterns)

## Exercise
Split the Chapter 7 extraction agent into an extraction agent and a separate validation agent that reviews its output.

## Deliverable
A two-agent pipeline with a clear handoff contract (schema) between them.
