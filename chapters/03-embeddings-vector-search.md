# Chapter 3: Embeddings & Vector Search Basics

*Phase 1 — Foundations Refresh*
## What you need to know

**What an embedding actually is.** An embedding model turns text into a fixed-length vector such that semantically similar text produces nearby vectors (measured by cosine similarity or dot product). It's a similarity tool, not a comprehension tool — an embedding tells you "these two pieces of text are about similar things," not "this text answers that question" or "this text is factually correct."

**When RAG helps.** Retrieval-augmented generation earns its complexity when you have a large, changing corpus of unstructured text and open-ended questions against it (support docs, internal wikis, research papers) — cases where you can't fit everything in context and don't know in advance which pieces are relevant.

**When RAG doesn't help.** If your task is structured-document extraction (a specific form, a specific record type) where you already know the shape of what you're looking for, RAG is usually the wrong tool — you want direct extraction (Chapters 2 and 7), not semantic retrieval. A common mistake is reaching for a vector database when a well-designed extraction prompt over the whole document would be simpler, cheaper, and more accurate. Ask "do I know what I'm looking for, or am I searching?" — extraction is the former, RAG is the latter.

**Index choice matters at scale, not at the start.** For a prototype, exact nearest-neighbor search (brute-force cosine similarity) is fine. Approximate indexes (HNSW, IVF) only start mattering once you're past tens of thousands of vectors and latency becomes a problem — don't over-engineer this on day one.

## Exercise

1. Stand up Postgres with the pgvector extension (or any vector store you prefer) on a scratch/test database.
2. Embed 20 sample documents (anything text-heavy you have — docs, notes, articles) using an embedding model.
3. Run 3 similarity queries against them and inspect the top results for relevance.
4. Write down, for your own target use case: is the underlying task "search across unstructured content" (RAG fits) or "extract known fields from a specific document" (RAG doesn't fit, use direct extraction instead)?

## Deliverable

A one-page note: where RAG would (and wouldn't) help in your target use case, with reasoning.

---
**Phase 1 milestone**: one-page note on which parts of your target use case are prompting problems vs. architecture problems.

## Insurance Claims Example
Your claims-handling guidelines, state-specific regulatory requirements, and coverage-interpretation notes are exactly the kind of large, evolving, unstructured corpus RAG is built for — "how do we handle a water-damage claim with a mold exclusion in Texas" is a real search problem. Contrast that with reading a specific police report or repair estimate: you already know the fields you're after (parties, damage description, estimated cost), so that's direct extraction (Chapter 7), not RAG. Try embedding a small set of claims-guideline documents and querying them, then write down which of your team's actual questions are "search the guidelines" vs. "extract from this one document."


## Resources
- [Building Intelligent Search with AI Embeddings, Neon, and pgvector](https://neon.com/guides/ai-embeddings-postgres-search)
- [The pgvector extension — Neon Docs](https://neon.com/docs/extensions/pgvector)
