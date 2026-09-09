# Chapter 4: RAG Architecture & When to Use It

*Phase 2 — Core GenAI Building Blocks*
## What you need to know

**The RAG pipeline has four failure points, not one.** Chunking (splitting documents into retrievable pieces), embedding (turning chunks into vectors), retrieval (finding the right chunks for a query), and generation (the LLM answering using retrieved chunks). A "RAG isn't working" complaint is almost always one of these four failing silently — diagnose which one before changing anything.

**Chunking strategy is the highest-leverage lever you have.** Naive fixed-size chunking (e.g. every 500 characters) frequently splits a sentence or table row across two chunks, destroying the information in both. Better defaults: chunk along natural document boundaries (headings, paragraphs, table rows), keep some overlap between adjacent chunks (so a boundary split doesn't lose context), and consider retrieving one chunk *plus* its neighbors rather than just the single best match.

**Retrieval evaluation is not optional.** Measure precision (of the chunks you retrieved, how many were actually relevant) and recall (of the relevant chunks that exist, how many did you retrieve) on a fixed set of test queries with known-correct answers. Without this, you're tuning chunking/retrieval blind.

**Hybrid search beats pure vector search in practice.** Vector similarity is good at "similar meaning," but weak at exact terms — model numbers, IDs, specific names. Combining vector search with traditional keyword/full-text search (and merging or re-ranking the results) consistently outperforms either alone for real-world corpora that mix prose with identifiers.

## Exercise

1. Build a minimal RAG pipeline over a small corpus of your own documents (product docs, notes — anything text-heavy).
2. Write 5 test questions with known-correct answers grounded in that corpus.
3. Run retrieval for each question and manually judge: did the retrieved chunks actually contain the answer? (This is your precision/recall check, done by hand at this scale.)
4. Pick one question that failed and diagnose which pipeline stage broke it — chunking, embedding, retrieval, or generation.

## Deliverable

A working RAG script, the 5 eval questions with pass/fail results, and a one-line root-cause note for any failure.

## Resources
- [Vector Search in Postgres — Neon Guides](https://neon.com/guides/vector-search)
- [Chunking Strategies for RAG: A Complete Guide](https://atlan.com/know/chunking-strategies-rag/)
