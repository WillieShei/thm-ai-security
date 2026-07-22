# Room 18 — Data Poisoning in RAG Systems

> Section 5 (Data Poisoning), Room 2 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). How poisoning corrupts training data, embeddings, and ingestion pipelines.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Data%20Poisoning-red)
![Frameworks](https://img.shields.io/badge/maps-OWASP%20LLM04-informational)

## Overview

Poisoning changes *what a model learns or retrieves*, not its code. This room covers training-data poisoning, embedding/vector-database poisoning, ingestion-pipeline abuse, and the behavioural-drift that makes subtle poisoning so hard to catch — ending in a hands-on knowledge-base poisoning lab.

## Learning objectives

- Explain training-data poisoning via gradient descent and why it persists after source removal
- Poison embeddings/vector DBs with keyword stuffing, semantic mimicry, and corpus flooding
- Abuse the ingestion pipeline
- Distinguish obvious effects from dangerous subtle behavioural drift

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Poisoning vs. code attacks |
| 2 | Training Data Poisoning | Gradient descent bias; Microsoft Tay |
| 3 | Embeddings & Vector Databases | Corpus flooding, semantic mimicry |
| 4 | Ingestion Pipeline Attacks | Automated, trusted pipelines |
| 5 | Impact on Model Behaviour | Behavioural drift; Waze ghost cars |
| 6 | Detection & Mitigation | Layered controls; Amazon fake reviews |
| 7 | Practical — PaperTrail | Knowledge-base poisoning (agent) |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/papertrail-poisoning.md`](./writeups/papertrail-poisoning.md)

## Key concepts

- **Training-data poisoning:** repeated poisoned samples bias weights via gradient descent (e.g., associating a product with negative sentiment). Small poisoned **fine-tuning** data has outsized effect. **Persists after source removal** (patterns, not files). Case study: Microsoft **Tay** (2016).
- **Embedding/vector poisoning:** similarity search ranks by closeness (cosine), not correctness.
  - *Keyword stuffing* · *semantic mimicry* (imitate trusted tone/structure) · *corpus flooding* (near-duplicate clusters raise top-k probability). Legitimate data stays but is out-ranked. Case study: a single poisoned doc in LangChain+Chroma+Llama 2 retrieved by ~80% of queries.
- **Ingestion pipeline:** collect → parse → chunk → embed → index → store — automated and trusted, so uploads/feeds/weak parsers multiply impact. Case study: dependency confusion (2021).
- **Behavioural drift:** obvious effects (backdoor triggers, persona shifts) vs. dangerous **subtle** poisoning (small bias, altered thresholds, omitted warnings) that's hard to separate from natural variance. Case study: Waze fake traffic / ghost cars.
- **Detection:** no single control — layer ingestion validation, guardrails, and behavioural-drift monitoring. Case study: Amazon blocked 250M+ suspected fake reviews (2023–24).

## Skills & mapping

`training-data poisoning` · `embedding/corpus poisoning` · `ingestion-pipeline abuse` · `behavioural-drift detection`

Role mapping: **AI red-teamer / ML integrity engineer**.

## Reference

- OWASP LLM04 Data & Model Poisoning: https://genai.owasp.org/llmrisk/llm04-data-and-model-poisoning/
