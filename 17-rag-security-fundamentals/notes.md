# Notes — RAG Security Fundamentals

## Task 2 — Architecture
- **Components:** embedding model (text→vectors), vector store (holds embeddings), retriever (similarity match), LLM (generates using retrieved context).
- **Flow:** query → embed → similarity search → top matches → injected into context → response.
- The model **never verifies** retrieved data. Numerical representation of text = **embeddings/vectors**; the component that selects docs = **retriever**.

## Task 3 — Attack Surface
- Four surfaces: ingestion, embedding generation, similarity retrieval, context injection.
- **Retrieval is highest-risk** — automatic, invisible; the model can't see source/intent or separate instructions from data.
- Lost during embedding: **context** (authorship / approval status).

## Task 4 — Retrieval Abuse & Context Manipulation
- **Passive poisoning** = plant & wait.
- **Active manipulation** = craft content to rank highly for sensitive queries.
- The model treats retrieved text as authoritative by placement; retrieval selects by semantic similarity/relevance.

## Task 5 — Real-World Failures
- Microsoft 365 Copilot email retrieval abuse (2026).
- ChatGPT plugins indirect prompt injection via external content (2023).
- Web-connected assistants serving stale content — governance gaps in the retrieval pipeline.

## Task 6 — Defensive Considerations
- Guardrails on retrieved content, ingestion validation/approval workflows, and behavioural monitoring for output drift. Defence-in-depth.
- Output drift = gradual influence from malicious/misleading data (not sudden failure); **behavioural monitoring** is the useful signal.
