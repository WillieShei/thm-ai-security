# Room 13 — Supply Chain Attack Vectors

> Section 4 (AI Supply Chain Security), Room 2 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). The **TryTrainMe breach** — investigate malicious serialisation, dependency confusion, repo manipulation, and API compromise.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Offensive%20Supply%20Chain-red)

## Overview

Walks the four attack layers through a single running breach (TryTrainMe), with hands-on analysis of a malicious pickle model and a compromised prompt template. Teaches *why* pickle is dangerous and how vectors combine.

## Learning objectives

- Explain how pickle `__reduce__` enables silent code execution, and why Keras Lambda attacks survive SafeTensors conversion
- Safely disassemble a malicious pickle model without executing it
- Recognize dependency confusion, typosquatting, and repo-token compromise
- Analyze an API/prompt-template compromise

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | The TryTrainMe breach |
| 2 | Malicious Model Files | Pickle `__reduce__`, Keras Lambda, GGUF |
| 3 | Investigating a Malicious Model | Lab: `pickletools` disassembly |
| 4 | Dependency Confusion | Highest-version-wins; Birsan 2021 |
| 5 | Model Repository Attacks | Typosquatting, fake orgs, stolen tokens |
| 6 | When Vectors Combine | All three at once |
| 7 | API Provider Compromise | Silent updates, prompt-template injection |
| 8 | Prompt Template Compromise | Agent lab: CommunityReview template |

Concept notes: [`notes.md`](./notes.md)
Walkthroughs: [`writeups/malicious-model-analysis.md`](./writeups/malicious-model-analysis.md) · [`writeups/prompt-template-compromise.md`](./writeups/prompt-template-compromise.md)

## Key concepts

- **Pickle `__reduce__`:** when saving a custom object, pickle calls `__reduce__`, which can return an arbitrary function + args that `pickle.load()` / `torch.load()` runs silently. The `os` module is the classic abused import; `REDUCE` is the opcode that executes the resolved function.
- **Architecture-level (Keras Lambda):** fires at **inference** time and **survives SafeTensors conversion** because the logic lives in the architecture, not the serialisation.

| Factor | Pickle `__reduce__` | Keras Lambda |
|--------|---------------------|--------------|
| Executes when | Model **loads** | Model **predicts** |
| Survives SafeTensors | No | **Yes** |
| Severity | CRITICAL (system commands) | MEDIUM (Python at inference) |

- **Dependency confusion:** `pip` installs the highest version across all indices, so a public package matching an internal name at version `99.0.0` wins (Alex Birsan, 2021 — Apple/Microsoft/PayPal, >$130k bounties). **Typosquatting** = misspelled names (`numppy`, `reqeusts`).
- **Repo attacks:** namespace/model typosquatting, fake trustworthy-sounding orgs, and compromise via stolen write-tokens (Lasso: 1,500+ HF tokens, 655 writable).
- **API compromise:** silent model updates, API-key theft, prompt-template injection, upstream training-data poisoning.

## Tools

`pickletools` (safe disassembly) · clean-vs-malicious model diffing · `safe_analysis.py` helper.

## Skills & mapping

`malicious pickle analysis` · `dependency-confusion detection` · `repo-attack recognition` · `prompt-template compromise analysis`

Role mapping: **AI red-teamer / ML supply chain security analyst**.

## Reference

- Alex Birsan, "Dependency Confusion": https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610
- MITRE ATLAS AML.T0010: https://atlas.mitre.org/techniques/AML.T0010
