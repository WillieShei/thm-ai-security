# Notes — AI Threat Modelling

Running case study: **MegaCorp** — RAG customer chatbot + recommendation engine + fraud detection.

## Task 2 — AI-Specific Assets & Attack Surfaces
- **Asset inventory:** training data, model weights/parameters, embedding vectors, system prompts, feature stores, model registries/artifacts — each with a "why it matters."
- Two AI behaviors that complicate modeling: **non-determinism** and the **black-box/explainability** problem.

## Task 3 — Data Supply Chain & STRIDE's Gaps
- **5-stage data supply chain:** collection → cleaning/labelling → training → validation/packaging → inference (security consideration at each).
- A compromised **model registry** can pass validation because backdoor triggers aren't in the validation set.
- **Slow-poisoning** scenario against MegaCorp's monthly-retrained fraud model.
- **STRIDE gaps for AI:** diffuse/delayed tampering, threats spanning multiple categories, expanded privilege from tool-using agents, and model extraction as a different kind of information disclosure.

## Task 4 — Adapting STRIDE for AI
- Full remap of all six categories (see README table), each with a concrete MegaCorp example: RAG KB poisoning, fraud-model drift, unexplainable regulatory decisions, competitor model extraction, denial-of-wallet, jailbreak-enabled PII exfiltration.
- Cited ATLAS IDs: AML.T0020 (data poisoning), AML.T0018 (backdoor), AML.T0024 (model extraction), AML.T0025.
- Still doesn't fit: adversarial examples, bias/fairness, emergent behavior.

## Task 5 — MITRE ATLAS
- Structure: tactics → techniques → sub-techniques → mitigations (ATT&CK-style, for AI/ML).
- Key techniques: Data Poisoning **AML.T0020**, Model Extraction **AML.T0024**, Evade ML Model **AML.T0015**, LLM Prompt Injection **AML.T0051** (direct vs. indirect), Backdoor ML Model **AML.T0018**.
- Workflow: **STRIDE to identify → ATLAS to enrich** with technique IDs + mitigations.
- Real case studies: **ShadowRay** (AML.CS0023, Ray framework) and **Morris II Worm** (AML.CS0024, self-replicating prompt-injection worm spreading via RAG email).

## Task 6 — OWASP LLM Top 10: Risk → Component
- Map all ten 2025 categories to the components they live in (LLM inference endpoint, vector DB/RAG pipeline, training pipeline, model registry, API gateway, tool integrations, frontend).
- **Bidirectional reading:** risk→component and component→risk (scope new risks when adding a component).
- MegaCorp's LLM inference endpoint alone carries **7 of 10** OWASP risks.

## Task 7 — Practical
- Select applicable OWASP LLM Top 10 vulns, map them to components, and justify each → flag. See writeup.

## Task 8 — Conclusion
- The end-to-end **repeatable workflow**: asset ID → data supply chain → STRIDE-AI → ATLAS enrichment → OWASP component mapping. Frames the three frameworks as complementary zoom levels.
