# Walkthrough — Threat Modelling MegaCorp's AI Assistant (Task 7)

> Graded practical: produce a justified, component-mapped vulnerability assessment for MegaCorp's AI assistant.
>
> **Note:** flag redacted per THM policy. Documents method.

## Objective

For MegaCorp's AI assistant, select the applicable OWASP LLM Top 10 vulnerabilities, map each to the specific architecture component it lives in, and justify the choice. A correct, justified assessment yields the flag.

## Approach — the repeatable workflow

1. **Asset identification.** List MegaCorp's AI assets: RAG knowledge base / vector store, LLM inference endpoint, system prompt, tool integrations, model registry, fraud model + training pipeline.
2. **STRIDE-AI pass.** Walk the six adapted STRIDE categories against those assets to surface candidate threats (e.g., RAG KB poisoning → Tampering; competitor model extraction → Information Disclosure; denial-of-wallet → DoS).
3. **ATLAS enrichment.** Attach technique IDs to each threat (Data Poisoning AML.T0020, Model Extraction AML.T0024, Prompt Injection AML.T0051, Backdoor AML.T0018) and note documented mitigations.
4. **OWASP component mapping.** For each vulnerability, identify the exact component:
   - Prompt injection / sensitive info disclosure / excessive agency → **LLM inference endpoint** (carries most of the risk).
   - Data/RAG poisoning → **vector DB / RAG pipeline**.
   - Backdoor / poisoning → **training pipeline / model registry**.
   - Unbounded consumption → **API gateway / inference endpoint**.
5. **Justify each selection** and submit → flag `THM{<redacted>}`.

## Techniques / concepts applied
- Multi-framework threat modeling (STRIDE-AI + ATLAS + OWASP)
- Risk→component mapping and justification
- Producing a prioritized, defensible assessment (the deliverable a security architect presents to a CISO)

## Result
Justified component-mapped assessment produced; flag captured. Output mirrors a real pre-deployment AI risk assessment report.
