# Walkthrough — UnIndexed (challenge)

> Audit "Atlas" for a retrieval-boundary failure.
>
> **Note:** flag and the restricted identifier are redacted per THM policy. Documents method.

## Objective

Determine whether Atlas enforces any access boundary on retrieval, and surface restricted board-level data if it does not.

## Method

1. **Baseline as a normal employee.** Ask ordinary questions to learn what public/authorised content looks like.
2. **Probe upward.** Ask about restricted, board-level topics (e.g., an emergency security fund) using natural phrasing so retrieval matches the confidential chunks.
3. **Observe the failure.** Atlas returns the internal reference identifier for a restricted item with **no access check** — retrieval is not scoped to the user's permissions.
4. **Capture the flag** derived from the disclosed restricted item. *(Redacted.)*

## Root cause
No pre-query access control on the shared index — the exact class of failure taught in Room 19. Retrieval has no boundary.

## Techniques / concepts applied
RAG boundary testing · retrieval-scope probing · identifying missing deterministic (pre-query) access control.
