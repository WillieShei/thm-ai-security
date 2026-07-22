# TryHackMe — Securing AI Systems

> Room 6 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). From "is the model safe?" to "is the **system architecture** safe?" — components, trust boundaries, OWASP LLM Top 10, and secure design patterns.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Architecture-blueviolet)
![Status](https://img.shields.io/badge/status-Completed-success)

## Overview

Written from the perspective of an **AI security architect**. The 2023 Samsung/ChatGPT leak frames the thesis: many AI incidents need no exploit — just architectural exposure. You learn to map an AI system's components and trust boundaries, classify risks against OWASP LLM Top 10 / MITRE ATLAS / NIST AI RMF, and design layered defenses before go-live.

## Learning objectives

- Decompose a production AI system into components and trust boundaries
- Classify AI risks with OWASP LLM Top 10, MITRE ATLAS, and NIST AI RMF
- Analyze system-level threats with concrete attack/defense pairs
- Apply defence-in-depth, least privilege, and MLSecOps
- Conduct a pre-deployment audit of an AI agent

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Model-safety → system-safety; Samsung leak |
| 2 | Anatomy of an AI System | 9 components, 5 trust boundaries, request trace |
| 3 | The AI Attack Surface | OWASP LLM Top 10, MITRE ATLAS, NIST AI RMF |
| 4 | System-Level Threats | 5 OWASP categories, attack/defense, CIA mapping |
| 5 | Secure Design Patterns | Defence-in-depth, least privilege, MLSecOps |
| 6 | Auditing TryAssist | Structured pre-deployment audit interview → flag |
| 7 | Conclusion | Recap + path roadmap |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/task6-tryassist-audit.md`](./writeups/task6-tryassist-audit.md)

## Architecture model (Task 2)

**Nine components:** UI · API gateway · orchestration layer · prompt construction · LLM · tool layer · output processing · logging/monitoring · vector store.

**Five trust boundaries:** user↔system · system↔LLM · LLM↔tools · system↔external data · system↔user.

## Governing frameworks (Task 3)

- **OWASP LLM Top 10 (2025)** — this room focuses on the five *system-architecture* categories: LLM02 Sensitive Information Disclosure, LLM05 Improper Output Handling, LLM06 Excessive Agency, LLM07 System Prompt Leakage, LLM10 Unbounded Consumption.
- **MITRE ATLAS** — adversary tactics (recon → impact).
- **NIST AI RMF** — Govern, Map, Measure, Manage (+ NIST AI 100-2 technical catalogue).

## Classification nuance (Task 4)

- Chevrolet chatbot case = **LLM01 Prompt Injection** (not Improper Output Handling).
- Air Canada case = **LLM09 Misinformation**.
- Excessive Agency's three sub-types: excessive functionality, permissions, autonomy (2023 ChatGPT plugin indirect injection).

## Skills & mapping

`trust-boundary mapping` · `OWASP LLM Top 10` · `NIST AI RMF` · `incident classification` · `least privilege / HITL` · `MLSecOps`

Primary role: **AI/application security architect**. Also **MLSecOps engineer**, **AI GRC analyst**, **AI red-teamer/auditor**.

## Reference

- OWASP Top 10 for LLM Applications: https://genai.owasp.org/
- NIST AI Risk Management Framework: https://www.nist.gov/itl/ai-risk-management-framework
- MITRE ATLAS: https://atlas.mitre.org/
