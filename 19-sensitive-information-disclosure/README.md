# Room 19 — Sensitive Information Disclosure

> Section 5 (Data Poisoning), Room 3 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). OWASP **LLM02** — how embeddings, retrieval, and weak access controls leak private data.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Data%20Leakage-red)
![Frameworks](https://img.shields.io/badge/maps-OWASP%20LLM02-informational)

## Overview

Where poisoning changes what's *learned* and injection changes *runtime instructions*, **disclosure exposes data that already exists**. This room covers the leak points in RAG systems — over-broad retrieval, shared vector DBs, verbose logging, weak metadata filtering — plus embedding inversion, membership inference, and deterministic access control.

## Learning objectives

- Classify disclosure under OWASP LLM02 and identify its leak points
- Explain embedding inversion and membership inference
- Understand top-k / metadata risks and multi-tenant leakage
- Apply segmentation, redaction, and pre-query access control

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Disclosure vs. poisoning vs. injection |
| 2 | OWASP LLM02 | Leak points |
| 3 | Common Disclosure Scenarios | Logging; EchoLeak, Proof Pudding |
| 4 | Attacks on Vector Databases | Embedding inversion, membership inference |
| 5 | RAG Retrieval Failures | top-k, filter-after-search, stale embeddings |
| 6 | Access Control & Segmentation | per-tenant/role index, metadata filtering |
| 7 | Best Practices | Redaction, allowlist, logging minimisation |
| 8 | Practical — Meridian Health | Shared-index leak + fixes (agent) |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/meridian-health-disclosure.md`](./writeups/meridian-health-disclosure.md)

## Key concepts

- **Leak points:** over-broad similarity search, shared vector DBs, large context windows, debug logging of full prompts, weak metadata filtering.
- **Logging risk:** storing full augmented prompts creates a secondary, broader-access data store.
- **Vector-DB attacks:** similarity by cosine/Euclidean; **embedding inversion** reconstructs text from vectors; **membership inference** confirms a record exists; multi-tenant stores leak if metadata filtering isn't applied **before** search.
- **Retrieval failures:** over-broad **top-k**, filtering applied *after* (not before) search, and stale/persistent embeddings from deleted docs. **Filtering must precede similarity search.**
- **Access control:** per-tenant index (strongest isolation, higher cost), per-role index, metadata-based filtering (common, error-prone). **Deterministic access control = filter before ranking**; prompt-based "only answer authorised docs" is *not* enforcement.
- **Best practices:** redaction at ingestion (NER/PII masking), allowlist retrieval filtering, logging minimisation (log IDs/hashes not content), data-retention (remove embeddings on delete), monitoring.

## CVEs / incidents referenced

- **EchoLeak** (CVE-2025-32711) — zero-click prompt injection via retrieved malicious email
- **Proof Pudding** (CVE-2019-20634) — model extraction via output/score probing
- **Milvus** Proxy auth bypass (CVE-2025-64513) — forged `sourceId` header
- **AnythingLLM** (CVE-2024-3033) — unauthenticated `/api/v/` namespace ops

## Skills & mapping

`OWASP LLM02` · `embedding inversion / membership inference` · `pre-query access control` · `redaction & logging minimisation`

Role mapping: **AI privacy engineer / RAG security engineer**.

## Reference

- OWASP LLM02 Sensitive Information Disclosure: https://genai.owasp.org/llmrisk/llm02-sensitive-information-disclosure/
