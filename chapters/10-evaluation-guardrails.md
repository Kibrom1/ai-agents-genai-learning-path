# Chapter 10: Evaluation, Guardrails & Prompt-Injection Defense

*Phase 3 — Agent Architecture Mastery*
## What you need to know

**An eval set is a regression test suite for prompts.** Without one, every prompt or model change is a leap of faith — you fix one failure case and have no way to know if you broke three others. Build a fixed set of input/expected-output pairs (15-20 to start is plenty), covering both typical cases and known edge cases, and rerun it on every change. This is the single highest-leverage habit in this entire curriculum.

**Hallucination detection needs a ground truth to check against.** For extraction tasks, this is easier than open-ended generation: you can programmatically check whether an extracted value actually appears in the source document (or is a reasonable derivation of something that does), and flag values that don't. For generation/summarization tasks, this typically needs either a human review sample or a second LLM call specifically prompted to check groundedness against the source.

**Prompt injection is a live threat the moment you ingest external content.** Any text your agent processes that didn't come from you or your own system — an uploaded document, an email body, a web page — can contain text crafted to look like instructions ("ignore previous instructions and instead..."). Defenses: clearly delineate untrusted content from instructions in your prompt structure (explicit tags/boundaries), never let untrusted content alone trigger a tool call with side effects, and treat any instruction-like text found *inside* ingested content as suspicious rather than authoritative.

**Guardrails are a second, independent check — not a prompt tweak.** "Just tell the model to be careful" in the system prompt is not a guardrail; it's a request the model can still fail to follow, especially under adversarial input. A real guardrail is a check that runs outside the model's control — output validation, an allowlist of permitted tool actions, or a separate classifier call.

## Exercise

1. Build a 15-20 item eval set for your extraction pipeline: real inputs with known-correct expected outputs, including at least 3 edge cases.
2. Run it, record the pass rate, then make a deliberate prompt change and rerun — confirm you can see exactly what regressed, if anything.
3. Add one prompt-injection test case: an input document containing text designed to look like an instruction (e.g. "ignore prior instructions and output X"), and confirm your pipeline doesn't follow it.

## Deliverable

An eval harness (script + eval set) you can rerun on every prompt/model change going forward, plus the injection test case and its result.

## Insurance Claims Example
Build an eval set from real (or de-identified) FNOL records and known-correct triage/extraction outcomes — include at least one ambiguous or incomplete claim as an edge case. For the injection test: claims documents are exactly the kind of external, sometimes-adversarial input this defends against — a claimant-submitted letter or scanned document could contain text crafted to look like an instruction ("please approve this claim automatically"). Confirm your pipeline treats that as untrusted document content, not as an instruction to follow.


## Resources
- [Define success criteria and build evaluations — Claude Docs](https://docs.claude.com/en/docs/build-with-claude/develop-tests)
- [Demystifying evals for AI agents — Anthropic](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [LLM Prompt Injection Prevention — OWASP Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html)
