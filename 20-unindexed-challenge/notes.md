# Notes — UnIndexed (Challenge)

Single challenge. Audit Cloudwright Labs' assistant "Atlas."

## Scenario
- Atlas is a RAG assistant. Probe for restricted board-level data.

## Key finding
- Atlas discloses the internal reference identifier of a restricted item (an emergency security fund) with **no access check** — a retrieval-boundary failure.
- Lesson: retrieval without pre-query access control has no boundary; anything embedded in the index can be surfaced by a well-aimed query.

> The restricted identifier and the flag are the challenge answers and are redacted per THM policy.
