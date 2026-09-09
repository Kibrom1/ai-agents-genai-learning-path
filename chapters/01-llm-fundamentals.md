# Chapter 1: LLM Fundamentals & Cost/Latency Tradeoffs

*Phase 1 — Foundations Refresh*
## What you need to know

**Tokens.** LLMs don't see characters or words — they see tokens, roughly 3-4 characters of English text each. A model's context window is a token budget, not a character budget, and it's shared between your input (prompt, retrieved documents, conversation history) and its output. Run a rough token count before you architect anything: a 20-page PDF is easily 15-20K tokens; a document extraction prompt with a few examples might be 1-2K tokens of overhead before you even see the target document.

**Sampling parameters.** `temperature` controls randomness (0 = deterministic-ish, higher = more varied); `top_p` truncates the sampling distribution to the most probable tokens. For extraction, classification, and anything where you want the same input to reliably produce the same output, keep temperature low (0-0.2). Save higher temperature for brainstorming or creative generation, where variety is the point.

**Model tiers exist for a reason.** Every provider ships small/fast/cheap models alongside large/slow/expensive ones. The mistake most people make is defaulting to the biggest model for everything. In practice: use a small model for routing, classification, and simple extraction; reserve the largest model for tasks that actually need deep reasoning (multi-step planning, ambiguous judgment calls, code generation). This isn't just a cost optimization — smaller models are often *more* reliable at narrow, well-specified tasks because they're less prone to over-elaborating.

**Cost and latency compound.** An agent that makes 5 sequential LLM calls per request multiplies both cost and latency by roughly 5x versus a single call. Every additional "let me double check that" step in an agent's reasoning loop is a real dollar and millisecond cost at scale — this matters more once you're past the prototype stage and into Chapter 11's routing/cost work.

## Exercise

1. Pick one real extraction or generation task (a document, an email, a support ticket — anything with a clear "right answer").
2. Write a single prompt for it and run it against two different model tiers from the same provider (a fast/cheap tier and a larger/more capable tier).
3. For each run, record: wall-clock latency, token count (input + output), and whether the output was correct.
4. Repeat the same prompt 3 times per tier at `temperature=0` and note whether outputs are identical or drift.

## Deliverable

A short table: model tier | cost per 1K tokens | latency | accuracy on your test case | output consistency at temperature=0.

## Resources
- [Claude models overview](https://docs.claude.com/en/docs/about-claude/models) — current model tiers, context windows, pricing
- [Prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) — covers tokens/context in practice
