# Walkthrough — Meridian Health Disclosure (Task 8)

> Agent lab: a RAG assistant on a single shared index leaks confidential HR data; fix it with pre-query access control and logging minimisation.
>
> **Note:** flags/answers redacted per THM policy. Documents method.

## Objective

Show that a shared vector index without access control leaks sensitive data, then remediate so public queries still work while confidential data is blocked.

## Method

1. **Confirm the safe baseline.** A public query (e.g., vacation policy) returns correctly.
2. **Probe for over-retrieval.** Ask about salary bands and CEO compensation — the shared index returns confidential chunks with no access check.
3. **Inspect the logs.**
   ```
   SHOW RETRIEVAL LOG
   ```
   Confidential chunks are logged **in full** — the log is a second leak surface.
4. **Trigger a semantic collision.** A benign benefits query surfaces a specific confidential HR record because similar embeddings rank together.
5. **Remediate — enable pre-query access control.**
   ```
   ENABLE ACCESS CONTROL
   ```
   Metadata filtering applied **before** similarity search blocks all three leaks while public data still resolves.
6. **Phase 2 — logging minimisation / redaction** so logs stop storing confidential content.

## Findings
- Root cause: no access control / over-broad retrieval on a shared index.
- The HR record appeared via **semantic collision**.
- Fixes: **deterministic (pre-query) access control** + **logging minimisation / redaction**.

## Techniques / concepts applied
Shared-index leakage analysis · semantic-collision recognition · pre-query metadata filtering · logging minimisation · defence-in-depth for RAG privacy.
