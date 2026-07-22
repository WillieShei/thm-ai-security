# Notes — Securing the AI Supply Chain

## Task 2 — Safe Serialisation
- **SafeTensors** (Hugging Face): JSON header + raw tensors only — no code execution.
- **PyTorch `weights_only=True`:** restricts the unpickler to tensor reconstruction (default since PyTorch 2.6).
- Limits: extension spoofing (**CVE-2023-6730**) and architecture-level attacks still apply.

## Task 3 — Model Verification & Provenance (lab)
- Verify integrity with **SHA-256** (`sha256sum` vs. `checksums.json` — one file won't match).
- Evaluate model cards: details, intended use, training data, performance, limitations.
- Treat **LoRA adapters** and conversion outputs as new artefacts.
- **Model Acquisition Framework (5 gates):** 1) Quarantine → 2) Source verification → 3) Integrity check → 4) Security scan → 5) Approve/reject. First step = **Quarantine**.

## Task 4 — Behavioural Analysis (agent)
- Model-load telemetry via a sandboxed subprocess with Python **audit hooks** (`sys.addaudithook()`) and a custom unpickler overriding `find_class()`.
- Clean load ≈ 5 events; malicious load shows a DANGEROUS `os` import, CRITICAL system calls (e.g., exfil of `/etc/passwd`), and returns a non-model object.

## Task 5 — Scanning Models Before Use (lab)
- **Fickling** (Trail of Bits): decompiles pickle bytecode without executing — `fickling --check-safety -p`.
- **ModelScan** (Protect AI): scans PyTorch/TF/Keras with severity levels; `os.system` = CRITICAL; SafeTensors = no issues.

## Tasks 6–7 — Architecture-Level Threats & Inspection (agent + lab)
- Keras **Lambda** layers run code at inference and survive format conversion.
- Architecture inspection enumerates layers; a compromised classifier shows an extra Lambda layer vs. the clean model.
- ModelScan's **`H5LambdaDetectScan`** flags Lambda as MEDIUM; `inspect_h5_model.py` (h5py) reveals the disguised layer name.

## Task 8 — Dependency Auditing & SBOMs (lab)
- Pin exact versions; lockfiles with hashes (`pip-compile --generate-hashes`, `poetry.lock`); scan with `pip-audit`.
- Private index via `index-url` with public PyPI as `extra-index-url`.
- Generate an **SBOM** with **Syft** (Anchore): **CycloneDX** (OWASP, security-focused) or **SPDX** (Linux Foundation, licence-focused).

## Task 9 — API Provider Assessment (agent)
- Four defences: provider due diligence, behaviour monitoring (baseline test prompts = the API equivalent of checksums), system-prompt governance, sandboxed evaluation (load → fixed prompt battery → adversarial probes → baseline comparison).
- A config using an external, unreviewed prompt returns the wrong policy and names the wrong provider — caught by baselining.
