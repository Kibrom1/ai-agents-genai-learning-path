# Chapter 7: Structured Extraction at Scale

*Phase 2 — Core GenAI Building Blocks*
## What you need to know

**Confidence scoring turns "the model said X" into "the model said X, and here's how sure it seems."** The simplest approach: ask the model to self-report a confidence level per extracted field alongside the value, and treat low-confidence fields differently downstream (flag for review rather than auto-accept). Self-reported confidence is imperfect but far better than none — it's the cheapest way to triage what needs a human look.

**Human-in-the-loop is a design decision, not a fallback.** Decide upfront: what confidence threshold auto-accepts a field vs. routes to a review queue? What happens to a record with a mix of high- and low-confidence fields — does the whole record wait, or only the flagged fields? This needs to be explicit in your data model (a `status` and `confidence` per field, not just per record), or review queues become unmanageable.

**Retry and fallback logic prevents one bad call from failing an entire pipeline.** A malformed response, a timeout, or an unexpectedly empty extraction should trigger a bounded retry (with backoff) before falling back to a lower-cost strategy (a smaller model, a simpler prompt, or routing to manual review) — never an unbounded retry loop, and never a silent failure that looks like a successful empty result.

**Extraction accuracy degrades on document variety, not document length.** A pipeline that works on 20 clean test documents can fail badly on the 21st because it has a layout or field convention you didn't test against. Build your eval set (Chapter 10) from real, messy, varied documents — not just the clean ones you happened to prototype with.

## Exercise

1. Pick one real extraction task from your own project (or a representative document type).
2. Implement it as an agent with tool calls, where the extraction includes a per-field confidence score.
3. Define a confidence threshold below which a field is flagged for review rather than auto-accepted.
4. Add a bounded retry with fallback for malformed/failed extraction attempts.
5. Compare the new pipeline's accuracy against whatever you had before (or a naive single-shot prompt as a baseline).

## Deliverable

Working spike + before/after accuracy comparison against the previous/baseline approach.

---
**Phase 2 milestone**: this spike, committed as a branch/PR (even if not merged).

## Resources
- [Extracting structured JSON — Claude Cookbooks (GitHub)](https://github.com/anthropics/claude-cookbooks/blob/main/tool_use/extracting_structured_json.ipynb)
- [Structured outputs — Claude Platform Docs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs) (revisit with a scale/confidence lens)
