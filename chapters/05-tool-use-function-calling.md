# Chapter 5: Tool Use & Function Calling

*Phase 2 — Core GenAI Building Blocks*
## What you need to know

**A tool is a contract, not just a function signature.** The model decides *whether* and *when* to call a tool based on its name, description, and parameter descriptions — these are prompt engineering, not just API plumbing. A poorly-described tool (`lookup(id)` with no explanation) gets called incorrectly or not at all; a well-described one (`look_up_vendor_by_name(name: str) -> returns vendor record with coverage status, or null if not found`) gets used correctly far more often.

**Design tools narrow, not broad.** A tool that does one clear thing is easier for the model to reason about and easier for you to test than one tool with five optional parameters covering five different behaviors. If you find yourself writing "if param X is set, do Y, otherwise do Z" inside a tool description, that's usually two tools.

**Handle malformed calls defensively.** Models occasionally call a tool with a missing required field, a hallucinated ID, or the wrong type. Your tool-execution code needs to validate inputs and return a clear error *back to the model* (not just throw an exception your agent loop crashes on) — a well-formed error message often lets the model self-correct on the next turn.

**Parallel vs. sequential.** When a task needs multiple independent lookups (e.g. "check the status of these three records"), parallel tool calls in one turn are faster and cheaper than one call per turn. When one call's result determines the next call's arguments, they must be sequential. Design your tool-execution loop to support both.

## Exercise

1. Define two tools against a small mock dataset: one that looks up a record by an identifier, and one that checks a status/attribute of a record.
2. Give an agent a question that requires chaining both — it must call the first tool, use the result to call the second.
3. Deliberately break one tool call (e.g. have it return an error for a bad ID) and observe whether the agent recovers or gets stuck.
4. Try a question that could be answered with two independent (parallel) calls and confirm your agent loop issues them together rather than one-by-one.

## Deliverable

An agent that correctly chains both tool calls for a multi-step query, plus a note on how it behaved when a tool call failed.

## Insurance Claims Example
Define two tools against a mock claims dataset: "look up policy by number" (returns coverage details, limits, deductible) and "check claim status" (returns current stage — FNOL received, assigned, under investigation, settled, closed). Give an agent a question that requires chaining both: "Is this loss covered under the policy, and what's the current status of the claim?" This is close to the first real conversational surface a claims agent needs — coverage lookup plus status, chained correctly, with a clear error path when a policy number doesn't match anything.


## Resources
- [Tool use with Claude — overview](https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview)
- [Programmatic tool calling](https://platform.claude.com/docs/en/agents-and-tools/tool-use/programmatic-tool-calling)
