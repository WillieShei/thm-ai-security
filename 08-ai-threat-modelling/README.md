# TryHackMe — AI Threat Modelling

> Room 8 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). Defender-focused, multi-framework methodology: AI asset inventory, STRIDE adapted for AI, MITRE ATLAS enrichment, and OWASP LLM Top 10 component mapping — applied end-to-end to one enterprise scenario.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Threat%20Modeling-blueviolet)
![Status](https://img.shields.io/badge/status-Completed-success)

## Overview

The most methodologically rigorous room in the path. Using a running **MegaCorp** case study (RAG customer chatbot + recommendation engine + fraud detection), it teaches a repeatable, three-framework workflow for pre-deployment AI risk assessment. This is essentially a compressed course in real AI security architecture consulting.

## Learning objectives

- Build an AI-specific asset inventory
- Map the AI data supply chain and understand STRIDE's gaps for AI
- Adapt all six STRIDE categories to AI-specific threats
- Enrich threats with MITRE ATLAS technique IDs
- Map OWASP LLM Top 10 risks to architecture components

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | MegaCorp scenario, defender framing |
| 2 | AI-Specific Assets & Attack Surfaces | Asset inventory + non-determinism/black-box |
| 3 | Data Supply Chain & STRIDE's Gaps | 5-stage data chain; slow-poisoning scenario |
| 4 | Adapting STRIDE for AI | Six categories remapped, with ATLAS IDs |
| 5 | MITRE ATLAS | Technique catalogue; ShadowRay, Morris II Worm |
| 6 | OWASP LLM Top 10 | Risk→component mapping |
| 7 | Practical | Threat-model MegaCorp's AI assistant → flag |
| 8 | Conclusion | The repeatable workflow |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/task7-megacorp-threat-model.md`](./writeups/task7-megacorp-threat-model.md)

## STRIDE, adapted for AI (Task 4)

| STRIDE | AI manifestation | ATLAS / OWASP |
|--------|------------------|----------------|
| **S**poofing | Data-source impersonation, RAG injection, model impersonation | — |
| **T**ampering | Data poisoning, model manipulation, prompt injection | AML.T0020 / AML.T0018 |
| **R**epudiation | No decision audit trail, model-version ambiguity | — |
| **I**nfo Disclosure | Model extraction, training-data extraction, embedding inversion | AML.T0024 / AML.T0025 |
| **D**enial of Service | Inference cost / "denial of wallet", GPU exhaustion, sponge examples | OWASP LLM10 |
| **E**levation of Privilege | Jailbreaking, excessive agency, tool exploitation | OWASP LLM06 |

Doesn't fit STRIDE: adversarial examples, model bias/fairness, emergent behavior (→ responsible-AI governance).

## The three frameworks as zoom levels

- **STRIDE** — wide-angle threat categories
- **MITRE ATLAS** — technical detail / technique IDs (Data Poisoning AML.T0020, Model Extraction AML.T0024, Evade ML Model AML.T0015, Prompt Injection AML.T0051, Backdoor AML.T0018) + case studies (ShadowRay AML.CS0023, Morris II Worm AML.CS0024)
- **OWASP LLM Top 10** — component mapping (the LLM inference endpoint alone carries 7 of 10 risks)

## Skills & mapping

`AI asset inventory` · `STRIDE-AI` · `MITRE ATLAS enrichment` · `OWASP component mapping` · `assessment reporting`

Primary role: **AI security architect / AI threat modeler**. Also **AI threat intelligence analyst**, **AI security program lead**.

## Reference

- MITRE ATLAS: https://atlas.mitre.org/
- OWASP Top 10 for LLM Applications: https://genai.owasp.org/
- Microsoft STRIDE: https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-threats
