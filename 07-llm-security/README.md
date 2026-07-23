# TryHackMe — LLM Security

> Room 7 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). A comprehensive, research-grounded tour of the LLM attack surface across four threat categories — with a live hands-on attack in every one.


## Overview

The most comprehensive LLM-specific attack reference in the path, organized into **data-based, model-based, system-based, and user-based** threats. Each category ends in a hands-on attack against a live simulated chatbot — closely mirroring real red-team methodology.

## Learning objectives

- Perform training-data extraction and membership inference
- Execute model extraction and model inversion attacks
- Exploit prompt injection as context-window poisoning, plus context overflow and memory poisoning
- Recognize LLM-powered social engineering and package-hallucination ("slopsquatting") supply-chain risk

## Task index

| # | Task | Threat category | Hands-on |
|---|------|-----------------|----------|
| 1 | Introduction | Taxonomy | — |
| 2 | Data-Based Threats | Data extraction, membership inference, prompt leakage | Membership inference attack |
| 3 | Model-Based Threats | Model extraction/theft, model inversion | Model inversion (reconstruct redacted data) |
| 4 | System-Based Threats | Context-window poisoning, overflow/DoW, memory poisoning | Memory poisoning attack |
| 5 | User-Based Threats | LLM social engineering, trust exploitation | Identify malicious hallucinated package |
| 6 | Conclusion | 10-threat cheat-sheet | — |

Concept notes: [`notes.md`](./notes.md)
Walkthroughs: [`writeups/`](./writeups/) (one per practical)

## The ten threats (Task 6 cheat-sheet)

Training-data extraction · membership inference · prompt/system-prompt leakage · model extraction · model inversion · context-window poisoning · context overflow · memory poisoning · LLM social engineering · trust exploitation (misinformation).

## Cited research & incidents

- GPT-2 verbatim training-data extraction study
- Mindgard extraction of ChatGPT-3.5-Turbo into a 100× smaller model for ~$50 API cost
- 2023 ChatGPT training-data extraction study
- Bing Chat "Sydney" system-prompt leak
- "Package hallucination" / **slopsquatting** against AI coding assistants

## Skills & mapping

`membership inference` · `model inversion` · `model extraction` · `memory poisoning` · `context overflow / DoW` · `slopsquatting awareness`

Primary role: **AI red-teamer / LLM penetration tester**. Secondary: **AI/ML privacy researcher** (data/model attacks), **secure software supply chain engineer** (package hallucination).

## Reference

- OWASP Top 10 for LLM Applications: https://genai.owasp.org/
- Extracting Training Data from LLMs: https://arxiv.org/abs/2012.07805
- MITRE ATLAS: https://atlas.mitre.org/
