# Walkthrough — Model Scanning & Architecture Inspection (Tasks 5–7)

> Statically scan a pickle model and inspect a Keras model's architecture for Lambda-layer threats.
>
> **Note:** flags/instance-specific values redacted per THM policy. Documents method + representative commands.

## Objective

Detect (a) a code-exec payload in a pickle model without executing it, and (b) a malicious Keras Lambda layer that survives format conversion.

## Static pickle scanning

1. **Fickling** — decompile bytecode without running it:
   ```bash
   fickling --check-safety -p suspicious_model.pkl
   ```
   Flags dangerous imports/calls (e.g., `os.system`).
2. **ModelScan** — multi-format scan with severity:
   ```bash
   modelscan -p suspicious_model.pkl
   ```
   An `os.system` call surfaces as **CRITICAL**; a SafeTensors file returns no issues.

## Architecture inspection (Keras / H5)

1. **ModelScan H5 Lambda detection** flags `Lambda` layers (MEDIUM) — these run Python at inference and survive SafeTensors conversion.
2. **Enumerate layers** with a helper:
   ```bash
   python3 inspect_h5_model.py pr_analyzer.h5
   ```
   The compromised model shows an **extra layer** (a disguised Lambda, e.g. a name like `normalize_output`) compared to the clean baseline.

## Method summary

1. Scan statically first (Fickling → ModelScan) — never load untrusted models.
2. If the format is Keras/H5, inspect the architecture too, because serialisation scanning alone won't catch Lambda-layer logic.
3. Diff layer counts/names against a known-clean baseline.

## Techniques / concepts applied
Static pickle decompilation (Fickling) · multi-format model scanning (ModelScan) · Keras architecture inspection (h5py) · defence against inference-time (Lambda) threats.
