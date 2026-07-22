# Walkthroughs — AI Recon & Enumeration (Tasks 2–4, 6)

> Hands-on offensive recon against the simulated **Cyphira** infrastructure, plus the blue-team SIEM exercise.
>
> **Note:** flags, real IPs, and exact credentials redacted per THM policy. Commands are illustrative of the method used in the room.

---

## Task 2 — Discovery with Nmap

**Goal:** find AI infrastructure on `10.10.45.0/24` and distinguish it from standard services.

**Method:**
1. Scan the subnet targeting AI-specific ports (Triton 8000-8002, TF Serving 8500-8501, TorchServe 8080-8082, MLflow 5000, Ray 8265, vector DBs, Jupyter 8888, MinIO 9000-9001).
   ```
   nmap -p 5000,8000-8002,8080-8082,8265,8500-8501,8888,9000-9001,11434,6333,19530 -sV 10.10.45.0/24
   ```
2. Compare open ports against the Task 2 reference table to label each host's role.
3. Note which services are AI infra vs. traditional (e.g., 8080 could be TorchServe *or* a generic web app — confirm by fingerprinting).

---

## Task 3 — Fingerprinting the framework

**Goal:** positively identify the framework behind each discovered port.

**Method:**
1. **HTTP headers:** `curl -I` and look for `Server` (TorchServe), `NV-Status` (Triton), uvicorn/FastAPI signatures, OpenAI-compatible `x-request-id`.
2. **JSON signatures:** hit a status/models endpoint and match the response shape (TF Serving vs. Triton vs. MLflow).
3. **Error fingerprinting:** send a malformed payload and read the framework-identifying error.
4. **gRPC:** `grpcurl -plaintext <host>:8001 list` (reflection) to dump the service schema.
5. **Endpoint naming:** probe `/predict`, `/invocations`, `/v1/models`, `/api/2.0/mlflow/`.

Result → framework identified per port; flag `THM{<redacted>}`.

---

## Task 4 — Enumeration for intelligence

**Goal:** turn "identification" into "intelligence" — extract real data from Cyphira.

**Method (MLflow chain):**
1. Search experiments → list registered models → search model versions (reveals artifact URIs + creator IDs) → search training runs (hyperparams, tags, Git commit hashes) → list artifacts.
2. Check FastAPI `/docs` and `/openapi.json`; try MLflow's GraphQL endpoint (can bypass REST auth).
3. Enumerate **Jupyter** for cleartext credentials (the room plants an MLflow password in a notebook).
4. Enumerate vector DBs (Weaviate schema, Qdrant collections/dimensions) and read Prometheus metrics as passive intel.

Extracted: experiment names, model stages, artifact URIs, a cleartext password → flag `THM{<redacted>}`.

---

## Task 6 — Blue-team: detect the recon

**Goal:** review simulated SIEM logs, classify each entry by recon phase, and recommend hardening.

**Method:**
1. Match log patterns to phases: enumeration request bursts, scripted MLflow access **without UI session cookies**, out-of-CIDR Prometheus scraping, AI-aware sequential port scans, MLflow path-traversal attempts, sessionless Jupyter API calls.
2. Recommend quick wins: enable MLflow auth, disable Jupyter `0.0.0.0` binding, block AI ports at the perimeter, disable Triton's model-control endpoint, restrict Prometheus to monitoring CIDRs, scope HF tokens, strip debug headers, audit S3/MinIO policies.

Result → phases classified + hardening recommended; flag `THM{<redacted>}`.

---

## Techniques / concepts applied
Network recon (Nmap + NSE) · service fingerprinting (curl/grpcurl, JA3/JA4) · MLflow/vector-DB enumeration · credential discovery · attack-surface mapping · SIEM detection engineering for AI-specific signatures.
