# Notes — Lockdown (Challenge)

Final room. Defensive capstone against Meridian's assistant "Bastion." Tools: `SHOW LOGS`, `QUERY AS: [name]`, `STATUS`.

## Three vulnerabilities → remediations
1. **Data retrieval** (confidential docs served) → document-level access control at retrieval time; metadata-based filtering **before** ranking.
2. **Logging** (plaintext sensitive content) → log redaction / data minimisation; log only non-sensitive metadata (IDs, timestamps).
3. **User-level access** (`QUERY AS` impersonation) → authenticated **server-side** identity + per-user access; derive identity from a verified session/token; scope every query to the user's permissions.

## Takeaway
Enforce security **before** the model sees data. Prompt-based access control is not enforcement; pre-query filtering and server-side identity are.

> Flag fragments/full flag are challenge answers and are redacted per THM policy.
