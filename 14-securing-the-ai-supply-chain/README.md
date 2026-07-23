# Room 14 — Securing the AI Supply Chain (SupplySecLab)

> Section 4 (AI Supply Chain Security), Room 3 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). Build defences for every gap exposed by the TryTrainMe breach.


## Overview

The defensive counterpart to Room 13. Covers safe serialisation, model provenance/integrity, sandboxed behavioural analysis, static model scanning, architecture inspection, and dependency/SBOM hygiene — organized around a repeatable **Model Acquisition Framework**.

## Learning objectives

- Migrate to safe serialisation (SafeTensors, `weights_only=True`)
- Verify model integrity and provenance (SHA-256, model cards, the 5-gate framework)
- Run sandboxed behavioural analysis with audit hooks
- Statically scan models with Fickling and ModelScan
- Inspect architecture for Lambda-layer threats
- Audit dependencies and generate an SBOM

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Defending the TryTrainMe gaps |
| 2 | Safe Serialisation | SafeTensors, `weights_only=True` |
| 3 | Model Verification & Provenance | SHA-256, model cards, 5-gate framework (lab) |
| 4 | Behavioural Analysis | Sandboxed audit hooks (agent) |
| 5 | Scanning Models Before Use | Fickling, ModelScan (lab) |
| 6–7 | Architecture-Level Threats & Inspection | Keras Lambda, h5py (agent + lab) |
| 8 | Dependency Auditing & SBOMs | pin/lock/hash, pip-audit, Syft (lab) |
| 9 | API Provider Assessment | Due diligence, baselining (agent) |

Concept notes: [`notes.md`](./notes.md)
Walkthroughs: [`writeups/model-scanning-and-inspection.md`](./writeups/model-scanning-and-inspection.md) · [`writeups/dependency-audit-sbom.md`](./writeups/dependency-audit-sbom.md)

## The Model Acquisition Framework (5 gates)

1. **Quarantine** — treat every new artefact as untrusted.
2. **Source verification** — provenance, org trust.
3. **Integrity check** — SHA-256 vs. `checksums.json`.
4. **Security scan** — Fickling / ModelScan.
5. **Approve / reject.**

Treat LoRA adapters and conversion outputs as **new artefacts** re-entering the framework.

## Key defences

- **Safe serialisation:** SafeTensors (JSON header + raw tensors, no code exec); PyTorch `weights_only=True` (default since 2.6). Limits: extension spoofing (CVE-2023-6730) and architecture-level attacks remain.
- **Behavioural analysis:** sandboxed subprocess + Python audit hooks (`sys.addaudithook()`) + custom unpickler overriding `find_class()`. A clean load ≈ 5 events; a malicious one shows a dangerous `os` import and system calls (e.g., exfil of `/etc/passwd`).
- **Static scanning:** **Fickling** (Trail of Bits) decompiles pickle bytecode without executing (`fickling --check-safety -p`); **ModelScan** (Protect AI) scans PyTorch/TF/Keras with severity (an `os.system` call = CRITICAL; SafeTensors = clean).
- **Architecture inspection:** ModelScan's `H5LambdaDetectScan` flags Lambda as MEDIUM; `inspect_h5_model.py` (h5py) reveals a disguised extra layer.
- **Dependency/SBOM:** pin exact versions; lockfiles with hashes (`pip-compile --generate-hashes`, `poetry.lock`); `pip-audit`; private index + public PyPI as `extra-index-url`; SBOM via **Syft** (CycloneDX = OWASP/security-focused, SPDX = licence-focused).

## Tools

`SafeTensors` · `Fickling` · `ModelScan` · `h5py` · `sha256sum` · `pip-audit` · `pip-compile`/`Poetry` · `Syft`

## Skills & mapping

`safe serialisation` · `provenance/integrity` · `sandboxed behavioural analysis` · `static model scanning` · `SBOM generation`

Role mapping: **MLSecOps / AI supply chain security engineer**.

## Reference

- SafeTensors: https://github.com/huggingface/safetensors
- Fickling: https://github.com/trailofbits/fickling
- ModelScan: https://github.com/protectai/modelscan
- Syft: https://github.com/anchore/syft
