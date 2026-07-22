# Notes — Supply Chain Attack Vectors

## Task 2 — Malicious Model Files
- **Pickle** serialises Python objects; saving a custom object calls **`__reduce__`**, which can return an arbitrary function + args that `pickle.load()` / `torch.load()` runs silently. Classic abused import: **`os`**.
- **Architecture-level (Keras Lambda):** runs code at **inference**, survives SafeTensors conversion (logic is in the architecture, not the serialisation).
- **GGUF:** not pickle-based, but weight-level backdoors baked in before quantisation still apply.

| Factor | Pickle `__reduce__` | Keras Lambda |
|--------|---------------------|--------------|
| Executes when | Model loads | Model predicts |
| Survives SafeTensors | No | Yes |
| Severity | CRITICAL | MEDIUM |

## Task 3 — Investigating a Malicious Model (lab)
- Never `pickle.load()` untrusted files. Disassemble safely with `python3 -m pickletools`.
- Red flags in the opcode stream: `SHORT_BINUNICODE 'os'`, `'system'`, `STACK_GLOBAL`, a beacon/`curl` string, and **`REDUCE`** (the opcode that executes the resolved callable).
- Compare against the clean model (which resolves a benign class). Helper `safe_analysis.py` gives a verdict.

## Task 4 — Dependency Confusion
- `pip` installs the **highest version across all indices**, so a public package matching an internal name at `99.0.0` wins.
- Alex Birsan (2021): hit Apple/Microsoft/PayPal, >$130k bounties.
- **Typosquatting:** misspelled names (`numppy`, `reqeusts`). Review with `pip-audit`.

## Task 5 — Model Repository Attacks
- Namespace/model typosquatting, fake trustworthy-sounding orgs, and compromise of legitimate repos via stolen write-tokens (Lasso: 1,500+ HF tokens, 655 writable).
- Warning signs: <500 downloads, no verify badge, sparse card, very recent upload, pickle-only.

## Task 6 — When Vectors Combine
- TryTrainMe used three at once: pickle payload (primary), an internal package name published publicly at `99.0.0` (backup / dependency confusion), and a fake trustworthy-sounding lab org (trust/repository manipulation).

## Task 7 — API Provider Compromise
- Silent model updates (swap the model behind the endpoint), API-key compromise, prompt-template injection, upstream training-data poisoning.
- A version-controlled prompt/system-prompt artefact can alter behaviour across every app that uses it.

## Task 8 — Prompt Template Compromise (agent lab)
- An assistant pulled a community prompt template that had been rewritten to **auto-approve everything**. Probing shows it approves changes it should reject and deflects responsibility. See writeup.
