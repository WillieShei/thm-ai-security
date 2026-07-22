# Notes — Sensitive Information Disclosure

## Task 2 — OWASP LLM02
- Disclosure exposes data that **already exists** (vs. poisoning = what's learned; injection = runtime instructions).
- Leak points: over-broad similarity search, shared vector DBs, large context windows, debug logging of full prompts, weak metadata filtering.

## Task 3 — Common Disclosure Scenarios
- Logging that stores full augmented prompts becomes a secondary, broader-access data store.
- Case studies: **EchoLeak** (CVE-2025-32711) — zero-click prompt injection via a retrieved malicious email; **Proof Pudding** (CVE-2019-20634) — model extraction via output/score probing.
- Retrieval mechanism = similarity search (cosine); count parameter = **top-k**.

## Task 4 — Attacks on Vector Databases
- Similarity by **cosine/Euclidean**.
- **Embedding inversion** — reconstruct text from vectors.
- **Membership inference** — confirm a record exists.
- Multi-tenant stores leak if metadata filtering isn't applied **before** search.
- Case study: Milvus Proxy auth bypass (CVE-2025-64513) — forged `sourceId` header.

## Task 5 — RAG Retrieval Failures
- Over-broad **top-k**, filtering applied **after** search, and stale/persistent embeddings from deleted docs.
- Filtering must **precede** similarity search. Increasing top-k increases exposure.

## Task 6 — Access Control & Segmentation
- Patterns: **per-tenant index** (strongest isolation, higher cost), **per-role index**, **metadata-based filtering** (common, error-prone).
- **Deterministic access control** = filter **before** ranking. Prompt-based "only answer authorised docs" is *not* enforcement.
- Logical grouping = namespace/collection.
- Case study: AnythingLLM (CVE-2024-3033) unauthenticated `/api/v/` namespace ops.

## Task 7 — Best Practices
- Redaction at ingestion (NER/PII masking).
- Allowlist retrieval filtering.
- Logging minimisation (log IDs/hashes, not content).
- Data-retention controls (remove embeddings on delete).
- Monitoring/detection.

## Task 8 — Practical: Meridian Health (agent)
- Single shared index, no access control. Public policy is fine; salary bands and CEO comp leak; retrieval logs store CONFIDENTIAL chunks in full; a benefits query surfaces a confidential HR record via semantic collision. Enabling metadata filtering **before** search blocks all three while public data still works. See writeup.
