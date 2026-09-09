# Chapter 2: Prompting Patterns & Structured Output

*Phase 1 — Foundations Refresh*
## What you need to know

**Roles matter.** Most LLM APIs separate a system prompt (persistent instructions — the model's job description) from user/assistant turns (the actual conversation or task). Put stable instructions (output format, constraints, persona, rules) in the system prompt; put the thing that changes per-call (the document, the question) in the user turn. Mixing these makes prompts harder to test and reuse.

**Few-shot beats zero-shot for anything with format ambiguity.** If you need a specific output shape, showing 2-3 examples of correct input→output pairs in the prompt is usually more reliable than describing the format in prose. This is especially true for extraction tasks with edge cases (missing fields, ambiguous values) — show the model an example of how you want those handled.

**Structured output is not optional for anything downstream of the LLM call.** If your code is going to parse the model's response, don't ask for prose and regex it — use the provider's native structured-output/tool-schema mechanism to constrain the output to a JSON schema. This eliminates an entire class of bugs (malformed JSON, missing fields, type mismatches) that free-text parsing is prone to.

**Prompt injection lives here too.** Any prompt that will later include user-supplied or document-supplied text needs to clearly delineate "instructions" from "data" (e.g. wrapping untrusted content in explicit tags) — this is Chapter 10's topic in depth, but the habit starts now: never format a prompt by directly concatenating untrusted text into the instruction portion.

## Exercise

1. Take a prompt from your own project (or any real task) that currently returns free text you parse yourself.
2. Rewrite it to define a strict JSON schema for the output and use your provider's native structured-output mechanism (not prompt-only "respond in JSON" instructions).
3. Add 2-3 few-shot examples covering at least one edge case (e.g. a missing/ambiguous field) and show the model the correct way to represent it.
4. Run both versions (old free-text vs. new structured) against 5-10 real inputs and compare parse-failure rate and field-level accuracy.

## Deliverable

Before/after prompt diff, plus a short accuracy/failure-rate comparison.

## Insurance Claims Example
Take a raw FNOL intake (a call transcript or web-form submission) and define a strict JSON schema for it: policy number, date/time of loss, loss type, loss description, injuries (Y/N), other parties involved, reported cause. Add few-shot examples covering an edge case adjusters actually see — a vague loss description ("something hit my car") or a claimant who doesn't know their policy number. Structured output here is what lets the intake step feed cleanly into coverage verification and triage downstream, instead of an adjuster re-typing free text.


## Resources
- [Prompt engineering overview](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview)
- [Structured outputs — Claude Platform Docs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)
- [Extracting structured JSON — Claude Cookbook](https://platform.claude.com/cookbook/tool-use-extracting-structured-json)
