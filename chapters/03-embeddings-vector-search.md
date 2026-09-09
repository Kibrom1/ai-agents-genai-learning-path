# Chapter 3: Embeddings & Vector Search Basics

*Phase 1 — Foundations Refresh*
## Learn
What embeddings actually encode, cosine similarity, and — importantly — when RAG helps vs. when it's unnecessary overhead for structured-document extraction.

## Resources
- [Building Intelligent Search with AI Embeddings, Neon, and pgvector](https://neon.com/guides/ai-embeddings-postgres-search)
- [The pgvector extension — Neon Docs](https://neon.com/docs/extensions/pgvector)

(pgvector on Postgres is used here as a concrete, low-friction default — swap in your vector DB of choice if you already have one.)

## Exercise
Enable pgvector on a scratch Postgres database, embed 20 sample documents, and run 3 similarity queries against them.

## Deliverable
A one-page note: where RAG would (and wouldn't) help in your target use case.

---
**Phase 1 milestone**: one-page note on which parts of your target use case are prompting problems vs. architecture problems.
