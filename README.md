# TryHackMe — AI Security Path (AI1)

Study notes and hands-on lab writeups for the full [TryHackMe AI Security path](https://tryhackme.com/aisecurity) — **21 rooms across offensive and defensive AI security**, from ML foundations through prompt injection, jailbreaking, AI infrastructure recon, supply chain security, and RAG data poisoning.

![Rooms](https://img.shields.io/badge/rooms-21-blue)
![Certificate](https://img.shields.io/badge/TryHackMe-AI%20Security%20(AI1)-brightgreen)
![Focus](https://img.shields.io/badge/focus-AI%20%2F%20LLM%20Security-red)

Each room is a folder with a `README.md` (overview, task index, skills, frameworks), a `notes.md` (per-task concept notes), and a `writeups/` folder with hands-on lab walkthroughs.

## Rooms

### Foundations & Threats
| # | Room | Focus | Difficulty |
|---|------|-------|------------|
| 01 | [Building Blocks of AI](./01-building-blocks-of-ai) | ML/DL/LLM foundations | Easy |
| 02 | [AI Security Threats](./02-ai-security-threats) | MITRE ATLAS, threats & defensive AI | Easy |
| 03 | [AI Models & Data](./03-ai-models-and-data) | AI/ML supply chain (data) | Medium |
| 04 | [Prompt Engineering](./04-prompt-engineering) | LLM control & instruction hierarchy | Easy |
| 05 | [AI Forensics](./05-ai-forensics) | AI-assisted DFIR | Medium |
| 06 | [Securing AI Systems](./06-securing-ai-systems) | AI security architecture | Medium |

### LLM Attack Surface
| # | Room | Focus | Difficulty |
|---|------|-------|------------|
| 07 | [LLM Security](./07-llm-security) | Full LLM attack surface | Medium |
| 08 | [AI Threat Modelling](./08-ai-threat-modelling) | STRIDE-AI, ATLAS, OWASP LLM Top 10 | Medium |
| 09 | [AI System Reconnaissance](./09-ai-system-reconnaissance) | AI infra discovery & enumeration | Medium |
| 10 | [Prompt Injection](./10-prompt-injection) | Direct & indirect injection | Medium |
| 11 | [Jailbreaking](./11-jailbreaking) | Safety/alignment red-teaming | Medium |

### Section 4 — AI Supply Chain Security
| # | Room | Focus | Difficulty |
|---|------|-------|------------|
| 12 | [Understanding AI Supply Chains](./12-understanding-ai-supply-chains) | Components, paradigms, attack layers | Easy |
| 13 | [Supply Chain Attack Vectors](./13-supply-chain-attack-vectors) | Pickle, dependency confusion, repos | Medium |
| 14 | [Securing the AI Supply Chain](./14-securing-the-ai-supply-chain) | SafeTensors, Fickling, ModelScan, SBOM | Medium |
| 15 | [Payload (challenge)](./15-payload-challenge) | Full incident investigation | Easy |
| 16 | [Checkpoint (challenge)](./16-checkpoint-challenge) | Multi-model go/no-go audit | Easy |

### Section 5 — Data Poisoning
| # | Room | Focus | Difficulty |
|---|------|-------|------------|
| 17 | [RAG Security Fundamentals](./17-rag-security-fundamentals) | RAG architecture & trust boundaries | Easy |
| 18 | [Data Poisoning in RAG Systems](./18-data-poisoning-in-rag-systems) | Training/embedding/ingestion poisoning | Medium |
| 19 | [Sensitive Information Disclosure](./19-sensitive-information-disclosure) | OWASP LLM02, embedding inversion | Medium |
| 20 | [UnIndexed (challenge)](./20-unindexed-challenge) | Retrieval-boundary audit | Medium |
| 21 | [Lockdown (challenge)](./21-lockdown-challenge) | Fix three RAG vulnerabilities | Medium |

## Consolidated skills matrix

| Domain | Skills demonstrated |
|--------|---------------------|
| **Foundations** | ML lifecycle, neural networks, transformers/attention, RLHF |
| **LLM offense** | Direct/indirect prompt injection, jailbreaking (roleplay, multi-turn/Crescendo, DAN), membership inference, model inversion/extraction, memory poisoning, context overflow / denial-of-wallet |
| **AI infra recon** | Service fingerprinting (Nmap, curl, grpcurl, JA3/JA4), MLflow enumeration, Shodan/Censys discovery, attack-surface mapping |
| **Supply chain** | Malicious pickle analysis (pickletools, Fickling), multi-format scanning (ModelScan), SafeTensors migration, SHA-256 provenance, dependency confusion/typosquatting, SBOM (Syft, CycloneDX/SPDX) |
| **RAG / data poisoning** | Corpus flooding, semantic mimicry, embedding-level poisoning, ingestion-pipeline abuse, behavioural-drift detection |
| **Data disclosure** | OWASP LLM02, embedding inversion, membership inference, pre-query access control, redaction, logging minimisation |
| **Threat modeling & architecture** | STRIDE-AI, OWASP LLM Top 10 (2025), MITRE ATLAS, NIST AI RMF, secure design patterns, MLSecOps |
| **Defensive / DFIR** | AI-assisted forensics, blue-team detection of AI recon, human-in-the-loop validation |

## Tools & frameworks referenced

**Analysis:** pickletools · Fickling · ModelScan · h5py · sha256sum · pip-audit · Syft · Nmap (+NSE) · grpcurl · ffuf/feroxbuster · MLOKit · Nuclei
**ML / RAG stack:** PyTorch · TensorFlow · Keras · scikit-learn · LangChain · Chroma · Milvus · Qdrant · Weaviate · MLflow · Hugging Face Hub
**Formats:** pickle (.pkl/.pt/.bin) · SafeTensors · Keras (.h5/.keras) · GGUF · CycloneDX/SPDX SBOMs
**Frameworks:** OWASP LLM Top 10 (2025) · MITRE ATLAS · STRIDE · NIST AI RMF · NIST CSF 2.0 · ISO/IEC 27090 · EU AI Act

## Repository layout

```
thm-ai-security/
├── README.md                 # this index
├── LICENSE                   # MIT
├── .gitignore
├── 01-building-blocks-of-ai/
│   ├── README.md
│   ├── notes.md
│   └── writeups/
├── 02-.../ … 21-.../
```

## A note on flags & THM policy

Writeups deliberately **redact flags, exact payloads, credentials, and machine-specific values**. TryHackMe's rules discourage publishing verbatim answers, and working exploit/jailbreak strings aren't included. The writeups document *methodology and reasoning* — which is what demonstrates competence to a reader (or recruiter).

## Publishing

This is a single portfolio monorepo — push the whole folder as one GitHub repository:

```bash
cd thm-ai-security
git init
git add .
git commit -m "TryHackMe AI Security path — notes and lab writeups (21 rooms)"
git branch -M main
git remote add origin git@github.com:<you>/thm-ai-security.git
git push -u origin main
```

---

*Compiled from the TryHackMe AI Security path (AI1). Original study/portfolio summaries — room narrative text paraphrased, not copied.*
