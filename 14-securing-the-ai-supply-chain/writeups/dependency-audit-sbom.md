# Walkthrough — Dependency Auditing & SBOM Generation (Task 8)

> Harden the Python dependency chain and produce a bill of materials.
>
> **Note:** flags/instance-specific values redacted per THM policy.

## Objective

Close the dependency-confusion / typosquatting gaps from the TryTrainMe breach and generate an auditable SBOM.

## Method

1. **Pin exact versions** — no floating ranges; a fixed version can't be silently overridden by a public `99.0.0`.
2. **Lockfiles with hashes** — hash-pinning rejects tampered artefacts:
   ```bash
   pip-compile --generate-hashes -o requirements.txt requirements.in
   # or use poetry.lock
   ```
3. **Audit for known vulns:**
   ```bash
   pip-audit -r requirements.txt
   ```
4. **Prefer a private index**, with public PyPI only as a fallback:
   ```
   --index-url https://pypi.internal.example/simple
   --extra-index-url https://pypi.org/simple
   ```
   (Note: `extra-index-url` still leaves confusion risk — private-first + pinning + hashes is the robust combination.)
5. **Generate an SBOM** with Syft:
   ```bash
   syft dir:. -o cyclonedx-json > sbom.cdx.json    # security-focused
   syft dir:. -o spdx-json > sbom.spdx.json        # licence-focused
   ```

## Key distinctions
- **CycloneDX** (OWASP) — security-focused SBOM.
- **SPDX** (Linux Foundation) — licence-focused SBOM.

## Techniques / concepts applied
Version pinning · hash-locked dependencies · `pip-audit` scanning · private-index configuration · SBOM generation (Syft, CycloneDX/SPDX).
