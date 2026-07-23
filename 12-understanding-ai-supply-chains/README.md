# Room 12 — Understanding AI Supply Chains

> Section 4 (AI Supply Chain Security), Room 1 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). Fundamentals of the AI supply chain, its attack surface, real incidents, and a model-vetting practical.



## Overview

Introduces the AI supply chain as an extension of the traditional software supply chain, with one new high-risk artefact: the **trained model** (architecture + training data + training process + serialised weights). Pickle-based model files can execute code at load time, and fine-tuning means **trust is inherited** from base models.

## Learning objectives

- Identify the four AI supply-chain components
- Distinguish the download vs. API consumption paradigms and their risk profiles
- Map the four attack layers and how they compound
- Vet a model repository and make a trust decision

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Model as a new supply-chain artefact |
| 2 | The Four Components | Datasets, Dependencies, Frameworks, Models |
| 3 | Consumption Paradigms | Download vs. API |
| 4 | The Four Attack Layers | Model, Dependency, Data, Infrastructure |
| 5 | Real-World Incidents | SolarWinds → NullifAI |
| 6 | Practical | "Should You Trust This Model?" |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/should-you-trust-this-model.md`](./writeups/should-you-trust-this-model.md)

## Key concepts

- **Four components:** Datasets · Dependencies · Frameworks · Models.
- **Two paradigms:** *Download* (you host the weights; file format drives risk — pickle = code exec, SafeTensors = safe, GGUF = no serialisation exploit but weight/quantisation risk) vs. *API* (only JSON crosses your boundary, but you trust the provider's hidden pipeline: training data, silent updates, system prompts, multi-tenant hosting).
- **Four attack layers:** Model (serialisation/architecture/weights) · Dependency (confusion, typosquatting) · Data (poisoning from ~0.1%, DoS as low as 0.001%) · Infrastructure (repo/account/CI-CD). They compound.
- **Inherited trust:** transfer learning / fine-tuning (incl. LoRA adapters) means backdoors in a base model survive downstream.

## Real-world incidents referenced

SolarWinds (2020, infra) · Log4Shell (2021, dependency) · PyTorch `torchtriton` dependency confusion (2022) · Hugging Face exposed tokens / ~100 malicious models (2023–24) · Ultralytics YOLO CI/CD cryptominer (2024) · @solana/web3.js npm cred theft (2024) · NullifAI scanner evasion (2025, model).

## Skills & mapping

`supply-chain mapping` · `paradigm risk analysis` · `attack-layer modeling` · `model vetting`

Role mapping: **AI/ML supply chain security analyst**, **third-party AI risk reviewer**.

## Reference

- OWASP LLM03 Supply Chain: https://genai.owasp.org/llmrisk/llm03-supply-chain/
- MITRE ATLAS AML.T0010 (ML Supply Chain Compromise): https://atlas.mitre.org/techniques/AML.T0010
