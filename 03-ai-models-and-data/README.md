# TryHackMe — AI Models & Data

> Room 3 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). AI/ML **supply chain security** — data provenance, training-data leakage, model-building trade-offs, fine-tuning inheritance, and the black-box problem.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Supply%20Chain-blueviolet)
![Status](https://img.shields.io/badge/status-Completed-success)

## Overview

The first **Medium**-rated room. It treats the AI build pipeline the way software supply chain security treats dependencies: every stage — data, training, fine-tuning, packaging — is an attack surface that needs review *before* deployment.

## Learning objectives

- Assess training-data sourcing and provenance risk
- Recognize PII/credential leakage in scraped corpora
- Understand how quantization and federated learning trade safety for efficiency
- Explain the fine-tuning "inheritance problem"
- Audit a model card and spot supply-chain red flags

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Data provenance, model-build decisions, black-box framing |
| 2 | Training Data | Sourcing categories, Common Crawl, provenance, ML-BOM, secrets leakage |
| 3 | Building the Model | Epochs/overfitting, pruning/quantization, federated learning |
| 4 | The Inheritance Problem | Fine-tuning risk, alignment erosion, base-model versioning |
| 5 | The Black Box Problem | Weights opacity, sampling vs. auditing, model cards |
| 6 | Practical | Audit a simulated Hugging Face-style repo → flag |
| 7 | Conclusion | Full data-to-deployment risk chain |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/task6-model-audit.md`](./writeups/task6-model-audit.md)

## Key concepts

- **Training-data sourcing:** web scraping, licensed datasets, synthetic data, internal corpora — each with a different trust profile. **Common Crawl** underlies GPT-3, DeepSeek, LLaMA.
- **Data provenance & ML-BOM:** extend SBOM practice (post-SolarWinds/EO 14028) into ML asset inventory. Truffle Security's scan of Common Crawl found ~12,000 live API keys/passwords.
- **Model-build trade-offs:** quantization can silently degrade safety alignment and defeat backdoor defenses tested only at full precision; federated learning improves privacy but invites gradient poisoning.
- **Inheritance problem:** fine-tuning can erode alignment with as few as ~10 adversarial examples (< $0.20, Stanford/Princeton), increase prompt-injection susceptibility (Cisco), and silently inherit upstream backdoors via untracked base-model versions.
- **Black box:** trained weights aren't human-readable; behavioral **sampling** (benchmarks, red-teaming) ≠ true **auditing**; **model cards** (Google, 2019) are the transparency artifact — but voluntary and often incomplete.

## Skills & mapping

`data provenance` · `ML-BOM / supply chain` · `secrets scanning` · `quantization/FL security` · `fine-tuning risk` · `model-card audit`

Role mappings: **AI/ML supply chain security analyst / third-party AI risk reviewer** (Tasks 2, 4, 5, 6), **ML security researcher** (Tasks 3–4).

## Reference

- MITRE ATLAS: https://atlas.mitre.org/
- Model Cards for Model Reporting: https://arxiv.org/abs/1810.03993
- TruffleHog (secrets scanning): https://github.com/trufflesecurity/trufflehog
