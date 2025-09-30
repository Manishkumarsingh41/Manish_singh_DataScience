# RAG-based AI Assistant — Notes

## 1. Design Trade-offs

- **Local vs Cloud**:  
  - The prototype is designed to run locally using free/open models and FAISS.  
  - Trade-off: Faster setup and no cloud costs vs. limited scalability for very large corpora.

- **Model Size vs Performance**:  
  - Used `sentence-transformers/all-MiniLM-L6-v2` for embeddings (small, fast, free).  
  - Used `google/flan-t5-small` for generation (lightweight, fast, free).  
  - Trade-off: Limited context understanding vs. low resource requirements.

- **Chunk Size**:  
  - Chunks of ~150 words with small overlap chosen to balance retrieval relevance and LLM token limits.  
  - Too large: may exceed LLM input limits.  
  - Too small: loss of context and reduced answer quality.

---

## 2. Retrieval Strategy

- **Document Chunking**:  
  - Text split into ~150-word chunks with 20–30 words overlap.  
  - Ensures context continuity and reduces loss of critical information.

- **Embedding Model**:  
  - `sentence-transformers/all-MiniLM-L6-v2` for dense vector representation.  
  - Efficient for large number of chunks and free to use.

- **Retrieval Method**:  
  - FAISS (dense vector search) for similarity search.  
  - Top-k chunks retrieved for each query (default k=3).  

- **Ensuring Relevance & Faithfulness**:  
  - Context chunks truncated to avoid LLM token overflow.  
  - Citations explicitly included in the prompt.  
  - Answers generated **only from retrieved chunks**, minimizing hallucinations.

---

## 3. Guardrails & Failure Modes

- **No Relevant Answers**:  
  - Returns graceful fallback message: `"No relevant information found."`

- **Hallucinations**:  
  - Answer generation limited to retrieved context.  
  - Citations enforced by prompt formatting.

- **Sensitive Queries** (optional):  
  - Filtering logic can be added to block inappropriate or sensitive queries.

- **Monitoring Metrics**:  
  - Precision@k, Recall@k for retrieval performance.  
  - Manual verification for answer faithfulness in the prototype phase.

---

## 4. Scalability Considerations

- **10x Increase in Documents**:  
  - FAISS scales well with dense vectors; chunk embedding generation can be batched.  

- **100+ Concurrent Users**:  
  - Local prototype may need cloud deployment (e.g., GPU instances) for real-time LLM inference.  
  - Use asynchronous query processing for higher throughput.

- **Cloud Deployment (Cost-efficient)**:  
  - Can use serverless or GPU-efficient solutions.  
  - Keep embedding index persistent; load LLM on demand.  

- **Future Improvements**:  
  - Hybrid retrieval (dense + BM25) for larger corpora.  
  - Advanced LLM models for better reasoning and longer context handling.  

---

**Author**: Manish Kumar Singh  
**Date**: 2025-09-30
