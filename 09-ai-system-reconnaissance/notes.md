# Notes — AI System Reconnaissance

## Task 1 — Introduction
- **Recon** = confirm what's deployed; **threat modeling** = assess what could go wrong.
- Real exposure: Shodan scan (Maor Dayan, Jan 2026) found **42,665** exposed AI agent instances, **93.4% vulnerable**; GreyNoise captured **91,000+** attack sessions targeting AI deployments.

## Task 2 — The AI Infrastructure Stack
- Port/protocol reference for 14 components (see README table): Triton, TF Serving, TorchServe, Ollama, vLLM, MLflow, Kubeflow, Ray, Qdrant, Weaviate, Milvus, Chroma, Jupyter, MinIO, Prometheus.
- Shodan dorks (e.g., `port:5000 "MLflow"`) tie to real IBM X-Force attack chains.
- Hands-on: **Nmap** against `10.10.45.0/24` with AI-specific port lists; distinguish AI infra from standard services.

## Task 3 — Fingerprinting AI Services
- **HTTP headers:** TorchServe `Server`, Triton `NV-Status` + GPU telemetry, uvicorn/FastAPI, OpenAI-compatible `x-request-id`.
- **JSON signatures:** TF Serving, Triton, MLflow, OpenAI-compatible endpoints.
- **Error fingerprinting:** malformed payloads trigger framework-identifying errors (MLflow path-traversal CVE-2024-1558; Databricks Mosaic Java exceptions).
- **Endpoint naming:** `/predict`, `/invocations`, `/v1/models`, MLflow `/api/2.0/mlflow/`.
- **gRPC:** `grpcurl` with reflection. **TLS:** JA3/JA4 (GreyNoise: 62 IPs / 27 countries shared one JA4H signature).
- Case study: GreyNoise campaign (Oct 2025–Jan 2026) sent innocuous prompts ("hi", geography Qs) at scale to fingerprint which LLM schema (OpenAI/Gemini/Anthropic) backed 73+ endpoints.
- Hands-on: fingerprint frameworks behind Cyphira ports with curl/grpcurl/malformed requests.

## Task 4 — Enumerating AI Systems
- **MLflow 5-step chain:** experiments search → registered models → model versions (artifact URIs, creator IDs) → training runs (hyperparams, tags, Git commits) → artifact listing.
- **Inference server metadata:** Triton/TF Serving config endpoints leak tensor shapes, dtypes, backends.
- **Vector DBs:** Weaviate schema/vectorizer, Qdrant collections/dimensions/point counts.
- **Prometheus** metrics = passive intel; **debug interfaces:** FastAPI `/docs`, `/openapi.json`, MLflow GraphQL bypassing REST auth; **Jupyter** cleartext creds.
- Case study: IBM X-Force Red chain (phishing → Jupyter cleartext MLflow creds → **MLOKit** enumeration → S3 exfil).
- Hands-on: extract experiment names, model stages, artifact URIs, and a cleartext Jupyter password from Cyphira.

## Task 5 — Mapping the AI Attack Surface
- Service-to-service trust; risk of binding to `0.0.0.0`.
- CVEs: MLflow hardcoded creds **CVE-2026-2635**, dir-traversal RCE **CVE-2026-2033** (both CVSS 9.8); Kubeflow without OIDC; TorchServe malicious `.mar` RCE; SageMaker DirectInternetAccess (82% of orgs, 2024).
- Supply chain: HF token leakage via GitHub dorks, dependency confusion, model-source poisoning.
- ATLAS: Active Scanning **AML.T0006**, Discover ML Artifacts **AML.T0007**, ML Supply Chain Compromise **AML.T0010**, Discover ML Model Family **AML.T0014** (Reconnaissance tactic **AML.TA0002**).
- Case study: **ShadowRay** (CVE-2023-48022) — Ray unauthenticated Job Submission API, 230k+ dashboards, XMRig; "ShadowRay 2.0" with LLM-generated malware/DDoS.

## Task 6 — Structured Methodology & Detection
- **5-phase methodology:** Passive Recon (Shodan/Censys/FOFA + GitHub dorks, AML.T0000) → Active Scanning (Nmap + NSE) → API Fingerprinting (ffuf/feroxbuster + AI wordlist) → Metadata Extraction (Task 4 chains) → Supply Chain Review.
- **Tooling:** Shodan/Censys/FOFA, GitHub dorks, Nmap NSE, grpcurl, ffuf/feroxbuster, curl, MLOKit, Nuclei, Agrus Scanner.
- **Blue team — SIEM signatures:** enumeration request bursts, scripted MLflow access without UI cookies, out-of-CIDR Prometheus scraping, AI-aware sequential port scans, MLflow path-traversal attempts, sessionless Jupyter API access.
- **Quick-win hardening:** enable MLflow auth, disable Jupyter `0.0.0.0` binding, block AI ports at perimeter, disable Triton model-control endpoint, restrict Prometheus to monitoring CIDRs, scope HF tokens, strip debug headers, audit S3/MinIO policies.
- Case study: June 2024 Hugging Face Spaces breach → token revocation, fine-grained tokens.
- Hands-on: classify SIEM entries by recon phase, recommend quick wins.

## Task 7 — Conclusion
- Cross-framework mappings: MITRE ATLAS; ATT&CK Enterprise (T1046, T1592, T1595.002); OWASP LLM (LLM05, LLM06, LLM03, LLM10); NIST AI RMF (Map/Measure sub-categories); NIST CSF 2.0 Identify (ID.AM, ID.RA).
