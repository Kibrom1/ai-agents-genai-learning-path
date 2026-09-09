# Chapter 12: Capstone — Document Intelligence Agent

*Phase 4 — Capstone Project*
## What you're building

The running example, end to end: an agent that takes a raw document, extracts and validates structured data (Chapter 7's pattern), cross-references an external data source, and flags anomalies for review — routed and logged through the control plane you designed in Chapter 11.

This chapter is applied integration, not new material. The point is combining everything from Chapters 4-11 into one working system rather than isolated exercises:

- **Ingestion**: accept a raw document (upload, email attachment, API payload).
- **Extraction**: pull structured fields with confidence scoring (Ch. 7).
- **Validation**: a second agent reviews the extraction against your defined rules, using the handoff contract from Ch. 9.
- **Cross-reference**: call out to an external data source (an API, a database, a public dataset) to enrich or verify the extracted data.
- **Anomaly flagging**: define what counts as "needs human review" — low confidence, a validation failure, or a cross-reference mismatch — and route those cases explicitly rather than letting them pass silently.
- **Routing & logging**: every LLM call in this pipeline goes through the control plane's routing policy and gets logged per the audit schema from Ch. 11.

## Exercise / Build steps

1. Wire the pieces from Chapters 5, 7, 8, and 9 together into one pipeline: ingest → extract → validate → cross-reference → flag.
2. Apply the Chapter 11 routing policy so each step uses the right model tier, and log every call per your audit schema.
3. Run the full pipeline against 10-20 real (or realistic synthetic) documents.
4. Review the flagged-for-review cases by hand — are they actually the ones that needed a human look, or is your confidence/validation threshold miscalibrated?

## Deliverable

An end-to-end working agent, tested on a sample of real (or realistic synthetic) documents, with a short note on what the anomaly-flagging threshold got right and wrong on that sample.
