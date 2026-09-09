# AI Agents / GenAI Apps — Learning Path

A self-directed, project-based learning path for going from software engineer to shipping production AI agent systems — modeled on Interview Kickstart's [EdgeUp Generative AI program](https://in.interviewkickstart.com/advanced-generative-ai-edgeup-course/) structure (phased curriculum, blended self-paced + hands-on build time, capstone projects, milestone reviews). Content and adaptation here are independently authored.

## Who this is for

Engineers with a solid software background (any stack) who want a structured, non-toy path into building GenAI agents and RAG systems — not an academic deep-learning course. You should be comfortable writing code and shipping software; no prior ML background required.

## Structure

5 phases, 16 chapters, roughly 10 weeks at 8–10 hrs/week.

| Phase | Chapters | Focus |
|---|---|---|
| 1 — Foundations Refresh | 1–3 | LLM fundamentals, prompting, embeddings |
| 2 — Core GenAI Building Blocks | 4–7 | RAG, tool use, agent frameworks, structured extraction |
| 3 — Agent Architecture Mastery | 8–11 | Memory/state, multi-agent orchestration, evals, cost & observability |
| 4 — Capstone Project | 12–13 | Build an end-to-end agent system |
| 5 — Production Hardening & Review | 14–16 | Security, cost audit, failure-mode review |

See [phase-plan.md](phase-plan.md) for the full phase breakdown and [chapters/](chapters) for chapter-by-chapter guides — each with resources, a hands-on exercise, and a concrete deliverable.

## Running example

Throughout the exercises we build one running project: a **Document Intelligence Agent** — an agent-based pipeline that ingests unstructured documents (invoices, compliance certificates, contracts, etc.), extracts structured data, validates it, cross-references an external data source, and flags anomalies for human review. It's deliberately generic — swap it for whatever real documents or workflow you have at your own job or product. The capstone (Chapters 12–13) is where this becomes a real, working system.

## How to use this

Work the chapters in order — each one assumes the deliverable from the previous chapter exists. Every chapter ends in something concrete (a script, a design doc, a working spike), not just reading. Chapters 12–13 assume Chapters 1–11 are done; don't skip ahead.

## Prerequisites

- Comfortable in at least one backend language/stack
- A Postgres instance you can experiment on (a free [Neon](https://neon.tech) project works well — used in the embeddings/RAG chapters)
- An API key for an LLM provider (examples throughout use the [Claude API](https://docs.claude.com), but the concepts transfer to any provider)

## Contributing

PRs welcome for corrected/updated resource links, additional exercises, or fixes. Open an issue first for structural changes (new chapters, reordering phases).

## License

MIT — see [LICENSE](LICENSE).
