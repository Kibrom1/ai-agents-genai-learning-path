# Chapter 13: Capstone — Apply It to a Second Domain

*Phase 4 — Capstone Project*
## What you're building

Take the pattern from Chapter 12 and rebuild it against a second, genuinely different use case — ideally something from your own job or product. This is the strongest proof the pattern generalizes rather than being a one-off script tuned to a single document type, and it should reuse the same infrastructure (control plane, eval harness) as Chapter 12 rather than starting from scratch.

Doing this surfaces the parts of Chapter 12 that were accidentally specific to the first domain — a chunking assumption, a validation rule, an extraction schema shape — versus the parts that were genuinely reusable. That distinction is worth more than the second working system itself.

## Exercise / Build steps

1. Pick a second document/data type meaningfully different in structure from Chapter 12's (different fields, different layout conventions, different validation rules).
2. Reuse the control plane, eval harness, and general pipeline shape from Chapter 12 — but adapt the extraction schema, validation rules, and cross-reference source to the new domain.
3. Note every place you had to change something that you expected to be reusable — that's a signal about what was over-fit to the first domain.
4. Run the eval harness against both domains and confirm the shared infrastructure (routing, logging, confidence thresholds) still performs sensibly on both.

## Deliverable

A second end-to-end working agent, sharing infrastructure with the Chapter 12 capstone, plus a short note on what turned out to be genuinely reusable vs. domain-specific.
