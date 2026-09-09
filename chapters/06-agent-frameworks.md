# Chapter 6: Agent Frameworks Survey & Standardization

*Phase 2 — Core GenAI Building Blocks*
## What you need to know

**"Agent" usually means a loop, not magic.** Strip away the branding and most agent frameworks are the same core loop: call the model with the current state and available tools → the model decides to respond or call a tool → execute the tool → append the result to state → repeat until done. Understanding this loop is more valuable than memorizing any one framework's API, because it's what lets you debug when a framework's abstraction leaks.

**Workflows vs. agents is a real distinction, not just terminology.** A *workflow* is a predefined sequence of LLM/tool calls you control in code (step A, then step B, then step C) — predictable, easy to test, easy to reason about failure modes. An *agent* lets the model decide the sequence of steps dynamically. Agents are more flexible but harder to test and debug. Most production systems are workflows with agent-like steps embedded where genuine dynamic decision-making is needed — not agents end-to-end. Default to a workflow; reach for a full agent loop only when the task genuinely requires the model to decide what to do next.

**Pick one and standardize.** LangGraph, hand-rolled loops, and provider-native agent SDKs all solve the same problem with different tradeoffs (LangGraph: rich ecosystem, more abstraction to learn; hand-rolled: full control, more code to maintain; provider SDKs: tight integration with one provider's tool-calling conventions). Chasing every new framework costs more than any framework's individual weaknesses — pick one for your team and go deep on it.

## Exercise

1. Rebuild the Chapter 5 two-tool agent using two different approaches — e.g. a graph-based framework and a hand-rolled loop.
2. For each, note: lines of code, how easy it was to add logging/tracing, and how easy it was to understand what the agent did when something went wrong.
3. Decide which approach you're standardizing on for your own work going forward.

## Deliverable

A one-paragraph decision record: chosen framework/approach and why, written so a future you (or a teammate) understands the tradeoff without re-deriving it.

## Resources
- [Building Effective AI Agents — Anthropic](https://www.anthropic.com/engineering/building-effective-agents) — read this one first, it's the conceptual foundation for the rest of this phase
- [Building agents with the Claude Agent SDK — Anthropic](https://anthropic.com/engineering/building-agents-with-the-claude-agent-sdk)
- [Workflows and agents — LangGraph Docs](https://docs.langchain.com/oss/python/langgraph/workflows-agents)
