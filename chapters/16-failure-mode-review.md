# Chapter 16: Failure-Mode Review & Go/No-Go

*Phase 5 — Production Hardening & Review*
## What you need to know

**"What happens when X fails" needs a specific, tested answer for every X — not a hope.** Walk through each of these explicitly for your capstone system, and confirm the actual behavior (don't just reason about it — trigger it and watch):

- **Low-confidence extraction**: does it correctly route to review rather than silently passing through as if it were high-confidence?
- **Model API outage or timeout**: does the pipeline retry sensibly (bounded, with backoff) and then fail loudly, or does it hang or silently drop the request?
- **Malformed input**: a corrupted file, an empty document, an unsupported format — does the pipeline reject it cleanly with a clear error, or does it produce a plausible-looking but garbage extraction?
- **Partial pipeline failure**: if step 3 of 5 fails (per Chapter 8's durable-execution work), does it actually resume correctly, or does this scenario only work in the chapter's original test?

**A go/no-go checklist forces you to answer these before production data is on the line, not after.** Treat any "we're not sure" answer as a no-go item, not an acceptable risk to carry forward silently.

## Do

Walk through each failure mode above against your actual capstone system (Chapters 12-13), triggering it deliberately rather than reasoning about it abstractly, and confirm the fallback behavior works as intended.

## Deliverable

A go/no-go checklist — each failure mode, its confirmed (tested, not assumed) behavior, and a go/no-go call before either capstone touches production data.

## Resources
- [Reliably run critical workflows — Inngest](https://www.inngest.com/docs/patterns/durable/reliably-run-critical-workflows) (retry/fallback patterns)
- [Building Effective AI Agents](https://www.anthropic.com/engineering/building-effective-agents) (failure-containment design)
