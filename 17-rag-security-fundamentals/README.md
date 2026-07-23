# Room 17 — RAG Security Fundamentals

> Section 5 (Data Poisoning), Room 1 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). How RAG works and where retrieval, context, and trust boundaries break.



## Overview

Retrieval-Augmented Generation grounds an LLM in retrieved documents — but the model never verifies what it retrieves. This room maps the RAG architecture and its attack surface, with **retrieval** identified as the highest-risk stage.

## Learning objectives

- Explain the four RAG components and the query→response flow
- Identify the RAG attack surface and why retrieval is highest-risk
- Distinguish passive poisoning from active manipulation
- Outline defence-in-depth for RAG

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Why RAG security matters |
| 2 | Architecture | Embedding model, vector store, retriever, LLM |
| 3 | Attack Surface | Ingestion, embedding, retrieval, context injection |
| 4 | Retrieval Abuse & Context Manipulation | Passive vs. active |
| 5 | Real-World Failures | M365 Copilot, ChatGPT plugins |
| 6 | Defensive Considerations | Guardrails, ingestion validation, monitoring |

Concept notes: [`notes.md`](./notes.md)

## Key concepts

- **Four components:** embedding model (text→vectors) · vector store (holds embeddings) · retriever (similarity match) · LLM (generates from retrieved context).
- **Flow:** query → embed → similarity search → top matches → injected into context → response. **The model never verifies retrieved data.**
- **Attack surface:** ingestion, embedding generation, similarity retrieval, context injection. **Retrieval is highest-risk** — automatic, invisible, and the model can't see source/intent or separate instructions from data.
- **Context lost during embedding:** authorship / approval status disappears, so retrieved text is treated as authoritative by placement.
- **Passive poisoning** (plant & wait) vs. **active manipulation** (craft content to rank highly for sensitive queries).

## Real-world failures

Microsoft 365 Copilot email retrieval abuse (2026) · ChatGPT plugins indirect injection via external content (2023) · web-connected assistants serving stale content (governance gaps in the retrieval pipeline).

## Skills & mapping

`RAG architecture` · `trust-boundary analysis` · `retrieval-abuse recognition` · `RAG defence-in-depth`

Role mapping: **AI application security engineer / AI red-teamer (RAG)**.

## Reference

- OWASP LLM01 Prompt Injection: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- OWASP LLM04 Data & Model Poisoning: https://genai.owasp.org/llmrisk/llm04-data-and-model-poisoning/
