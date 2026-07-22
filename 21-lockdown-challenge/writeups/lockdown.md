# Walkthrough — Lockdown (challenge)

> Defensive capstone: fix three RAG vulnerabilities in "Bastion." Each correct remediation yields a flag fragment.
>
> **Note:** flag fragments redacted per THM policy. The remediations below are legitimate security practices, documented in full.

## Objective

Reproduce and remediate three vulnerabilities, verifying each with `SHOW LOGS`, `QUERY AS: [name]`, and `STATUS`.

## Vulnerability 1 — Data retrieval (confidential docs served)
1. Reproduce: a normal query returns confidential documents.
2. Remediate: enforce **document-level access control at retrieval time** — apply metadata-based filtering **before** ranking so unauthorised chunks are never candidates.
3. Verify with `QUERY AS` a low-privilege user → confidential docs no longer returned.

## Vulnerability 2 — Logging (plaintext sensitive content)
1. Reproduce: `SHOW LOGS` reveals full sensitive content stored in the clear.
2. Remediate: **log redaction / data minimisation** — store only non-sensitive metadata (IDs, timestamps), never raw retrieved content.
3. Verify: `SHOW LOGS` now shows redacted entries.

## Vulnerability 3 — User-level access (`QUERY AS` impersonation)
1. Reproduce: `QUERY AS: [name]` lets you assume another user's identity client-side.
2. Remediate: **authenticated server-side identity + per-user access** — derive identity from a verified session/token, never from a client-supplied name; scope every query to that user's permissions.
3. Verify: impersonation attempts are rejected; each user only retrieves what they're entitled to.

## Result
All three remediated; flag reconstructed from the three fragments. *(Redacted.)*

## Techniques / concepts applied
Pre-query metadata access control · log redaction / data minimisation · server-side identity enforcement · layered RAG defence ("enforce before the model sees data").
