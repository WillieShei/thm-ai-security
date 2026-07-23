# TryHackMe — AI System Reconnaissance

> Room 9 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). The most offensive, tool-heavy room: discovering, fingerprinting, and enumerating real AI infrastructure — then seeing what it all looks like from the defender's SIEM.


## Overview

Reconnaissance = confirming what's *actually deployed* (vs. threat modeling's "what could go wrong"). Grounded in real 2025–2026 campaigns and CVEs, nearly every task is hands-on with real tools (Nmap, curl, grpcurl) against simulated **Cyphira** infrastructure. Task 6 flips to blue-team: analyze your own recon in SIEM logs and recommend hardening.

## Learning objectives

- Recognize AI infrastructure by port/protocol and fingerprint the framework behind each service
- Enumerate MLflow, inference servers, and vector databases for intelligence
- Map findings into a full attack surface with real CVEs
- Apply a repeatable 5-phase recon methodology
- Detect AI-recon signatures in SIEM logs and recommend quick-win hardening

## Task index

| # | Task | What it covers | Hands-on |
|---|------|----------------|----------|
| 1 | Introduction | Recon vs. threat modeling; Shodan exposure stats | — |
| 2 | The AI Infrastructure Stack | Port/protocol reference (14 components) | Nmap vs. 10.10.45.0/24 |
| 3 | Fingerprinting AI Services | HTTP/JSON/error/gRPC/JA3-JA4 fingerprinting | curl/grpcurl framework ID |
| 4 | Enumerating AI Systems | MLflow chain, metadata, vector DBs, MLOKit | Extract creds/artifacts |
| 5 | Mapping the AI Attack Surface | Real CVEs; ShadowRay; ATLAS mapping | — |
| 6 | Recon Methodology & Detection | 5-phase playbook; blue-team SIEM view | Classify SIEM logs, harden |
| 7 | Conclusion | Cross-framework mappings | — |

Concept notes: [`notes.md`](./notes.md)
Walkthroughs: [`writeups/`](./writeups/)

## AI infrastructure port cheat-sheet (Task 2)

| Service | Port(s) |
|---------|---------|
| NVIDIA Triton | 8000/8001/8002 |
| TensorFlow Serving | 8500/8501 |
| TorchServe | 8080/8081/8082 |
| Ollama | 11434 |
| vLLM | 8000 |
| MLflow | 5000 |
| Ray dashboard | 8265 |
| Qdrant | 6333/6334 |
| Weaviate | 8080 |
| Milvus | 19530 |
| Chroma | 8000 |
| Jupyter | 8888 |
| MinIO | 9000/9001 |
| Prometheus | 9090 |

## Real CVEs & campaigns referenced

- **ShadowRay** (CVE-2023-48022) — Ray's unauthenticated Job Submission API; 230k+ exposed dashboards; XMRig cryptomining; "ShadowRay 2.0" with LLM-generated malware
- **MLflow** path traversal CVE-2024-1558; hardcoded creds CVE-2026-2635; directory-traversal RCE CVE-2026-2033 (CVSS 9.8)
- GreyNoise LLM-fingerprinting campaign (Oct 2025–Jan 2026), shared JA4H signature
- IBM X-Force ML attack chain (phishing → Jupyter creds → MLOKit → S3 exfil)
- June 2024 Hugging Face Spaces breach

## Tooling

`Nmap (+NSE)` · `curl` · `grpcurl` · `ffuf/feroxbuster` · `Shodan/Censys/FOFA` · `GitHub dorks` · `MLOKit` · `Nuclei` · `Agrus Scanner`

## Skills & mapping

`AI infra discovery` · `service fingerprinting` · `MLflow enumeration` · `attack-surface mapping` · `blue-team detection`

Primary role: **AI/ML infrastructure penetration tester / red-teamer**. Secondary: **detection engineer / SOC analyst** (Task 6 blue-team), **GRC analyst** (Task 7 cross-framework mapping).

## Reference

- MITRE ATLAS: https://atlas.mitre.org/
- Shodan: https://www.shodan.io/
- MLflow security: https://mlflow.org/docs/latest/auth/
