
# Retrieval Pipeline Architecture

## 1. Overview

The retrieval pipeline is responsible for identifying relevant
information from the indexed enterprise knowledge base based
on user queries.

It retrieves relevant document chunks, combines different
retrieval strategies, reranks candidates and constructs
context for grounded LLM generation.

## 2. Query Processing

The query processing component receives user questions.

Responsibilities:

- Validate incoming queries.
- Normalize query text.
- Generate query embeddings.
- Apply document access restrictions.
- Support query rewriting when necessary.

## 3. Dense Retrieval

Dense retrieval uses vector embeddings to identify
semantically relevant document chunks.

The query is converted into an embedding using the
same embedding model and compatible configuration
used during document indexing.

Milvus performs vector similarity search.

## 4. Sparse Retrieval

Sparse retrieval uses keyword-based matching.

BM25 will initially be used for identifying documents
containing relevant keywords and technical terminology.

This is particularly useful for:

- API names
- Error codes
- Product identifiers
- Technical terminology
- Exact phrases

## 5. Hybrid Retrieval

The system combines dense and sparse retrieval.

Reciprocal Rank Fusion (RRF) will initially be evaluated
as the ranking fusion strategy.

The purpose is to combine semantic relevance with
keyword-based relevance.

## 6. Reranking

Retrieved candidates will be passed to a reranking model.

A locally hosted cross-encoder will initially be evaluated.

The reranker evaluates query-document relevance
and produces an improved candidate ranking.

## 7. Context Construction

The context construction component prepares retrieved
information for LLM generation.

Responsibilities:

- Remove duplicate chunks.
- Preserve document provenance.
- Respect context window limits.
- Apply token-budget constraints.
- Preserve source and page references.
- Enforce document access restrictions.

## 8. Grounded Generation

The selected context and user query are passed
to an external LLM API.

The generation component must:

- Use retrieved evidence.
- Avoid unsupported claims.
- Provide source citations.
- Handle insufficient evidence.
- Follow a controlled response format.

## 9. Retrieval Evaluation

Retrieval quality will be evaluated using:

- Precision@K
- Recall@K
- Mean Reciprocal Rank (MRR)
- Normalized Discounted Cumulative Gain (NDCG)

Generation quality will be evaluated separately.

## 10. Performance and Monitoring

Track:

- Query processing latency.
- Dense retrieval latency.
- Sparse retrieval latency.
- Reranking latency.
- Number of retrieved candidates.
- Context token count.
- LLM API latency.
- Token consumption and cost.

## 11. Future Enhancements

- Query expansion.
- Multi-query retrieval.
- Metadata-aware retrieval.
- Parent-child retrieval.
- Contextual compression.
- Advanced reranking strategies.
- Adaptive retrieval.

## 12. Design Principle

The retrieval pipeline must prioritize relevance,
traceability, access control and evidence-grounded
answer generation.
