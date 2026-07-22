# Notes — Securing AI Systems

## Task 1 — Introduction
- Shift from **model-level** ("is AI safe?") to **system-level** ("is this architecture safe?").
- **2023 Samsung/ChatGPT leak** — no exploit needed, just architectural exposure of sensitive data.

## Task 2 — Anatomy of an AI System
- Traditional apps = deterministic/structured; AI-augmented = probabilistic/unstructured.
- **Nine components:** UI, API gateway, orchestration layer, prompt construction, LLM, tool layer, output processing, logging/monitoring, vector store.
- **Five trust boundaries:** user↔system, system↔LLM, LLM↔tools, system↔external data, system↔user.
- Practice: trace a single request end-to-end across every boundary (data-flow diagramming, STRIDE-style).

## Task 3 — The AI Attack Surface
- **OWASP LLM Top 10 (2025):** five system-architecture categories for this room — LLM02 (Sensitive Info Disclosure), LLM05 (Improper Output Handling), LLM06 (Excessive Agency), LLM07 (System Prompt Leakage), LLM10 (Unbounded Consumption).
- **MITRE ATLAS** — adversary tactics (recon → impact), the ML counterpart to ATT&CK.
- **NIST AI RMF** — four functions: Govern, Map, Measure, Manage; + NIST AI 100-2 technical catalogue.

## Task 4 — System-Level Threats (attack/defense pairs)
- **LLM10 Unbounded Consumption** — cost/resource exhaustion → rate limiting, quotas.
- **LLM07 System Prompt Leakage** — real extractions (ChatGPT, Bing, Gemini, custom GPTs) → never embed secrets in prompts.
- **LLM05 Improper Output Handling** — defense via parameterized queries. *Classification nuance:* Chevrolet chatbot = LLM01 Prompt Injection; Air Canada = LLM09 Misinformation.
- **LLM06 Excessive Agency** — sub-types: excessive functionality / permissions / autonomy; 2023 ChatGPT plugin indirect injection → least privilege + human-in-the-loop.
- **LLM02 Sensitive Information Disclosure** — Samsung revisited → PII stripping, encryption.
- Map all five to the **CIA triad**.

## Task 5 — Secure Design Patterns
- **Defence in depth** mapped to each trust boundary.
- **Least privilege:** read-only-by-default DB access, scoped API tokens, tool allowlisting, HITL for state-changing ops.
- **Input/output validation** for free-form text: length limits, injection-pattern flagging, output schema constraints.
- **Monitoring/observability:** request patterns, token consumption, tool invocations, response anomalies, prompt-extraction attempts, cost metrics.
- **MLSecOps:** shift security left across the ML lifecycle.

## Task 6 — Auditing TryAssist
- Non-adversarial **pre-deployment audit interview** of a simulated AI agent using five due-diligence questions (capabilities, permissions, autonomy, instructions, data retention); map each finding to an OWASP category. See writeup.

## Task 7 — Conclusion
- Recap of architecture, frameworks, threats, controls. Candid note: "some recommendations were implemented. Not all of them" — real security-vs-rollout friction.
- Roadmap: LLM Security, AI Threat Modelling (STRIDE, PASTA), AI System Reconnaissance, plus Supply Chain, Prompt Security, Data Poisoning modules.
