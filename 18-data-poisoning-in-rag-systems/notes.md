# Notes — Data Poisoning in RAG Systems

## Task 2 — Training Data Poisoning
- Attackers change *what the model learns*, not its code. Repeated poisoned samples bias weights via **gradient descent** (e.g., associating a product with negative sentiment).
- **Pre-training vs. fine-tuning:** small poisoned fine-tune data has outsized effect.
- **Persists after source removal** — the model learned patterns, not files.
- Case study: Microsoft **Tay** (2016). Poisoning that affects training = **training-data poisoning**.

## Task 3 — Embeddings & Vector Databases
- Similarity search ranks by closeness (**cosine**), not correctness.
- **Corpus poisoning techniques:**
  - *Keyword stuffing.*
  - *Semantic mimicry* — imitate trusted tone/structure.
  - *Corpus flooding* — near-duplicate clusters raise top-k probability.
- Legitimate data stays but is **out-ranked**. Case study: single poisoned doc in LangChain+Chroma+Llama 2 retrieved by ~80% of queries.
- Vector-space manipulation without retraining = **embedding-level poisoning**.

## Task 4 — Ingestion Pipeline Attacks
- Pipeline = collect → parse → chunk → embed → index → store; usually automated and trusted.
- Attackers upload/modify docs, inject into feeds, or exploit weak parsers; automation multiplies impact.
- Case study: dependency confusion (2021).

## Task 5 — Impact on Model Behaviour
- Obvious effects (backdoor triggers, persona shifts) vs. dangerous **subtle** poisoning (small bias, altered thresholds, omitted warnings) = **behavioural drift**, hard to separate from natural variance.
- Case study: Waze fake traffic / ghost cars. Corrupted while infra stays up = input/data.

## Task 6 — Detection & Mitigation
- No single control; layer ingestion validation, guardrails, and behavioural-drift monitoring.
- Monitoring for gradual output changes = **behavioural monitoring**.
- Case study: Amazon layered detection blocked **250M+** suspected fake reviews (2023–24).

## Task 7 — Practical: PaperTrail (agent)
- Observe normal answer → inject a poisoned "policy revision" into the knowledge base → re-ask and confirm the assistant repeats the weakened policy. No weights/prompt changed. See writeup.
