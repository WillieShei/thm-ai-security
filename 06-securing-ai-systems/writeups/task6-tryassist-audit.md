# Walkthrough — Auditing TryAssist (Task 6)

> A structured, **non-adversarial** pre-deployment audit: interview a simulated AI agent about itself, then map findings to OWASP LLM Top 10.
>

## Objective

Conduct a due-diligence audit of the TryAssist agent by asking five standard audit questions, then classify each finding against the OWASP categories from Task 4. Completing the audit yields the flag.

## Approach — the five audit questions

Unlike the earlier prompt-injection labs, this is legitimate due diligence, not an attack. Ask the agent about:

1. **Capabilities** — what tasks/tools can it actually perform? (surfaces LLM06 Excessive Functionality)
2. **Permissions** — what access does it hold (DB, APIs, filesystem)? (LLM06 Excessive Permissions; LLM02 if it can reach sensitive data)
3. **Autonomy** — can it take state-changing actions without approval? (LLM06 Excessive Autonomy — is there a human-in-the-loop?)
4. **Instructions** — what are its system instructions, and would it disclose them? (LLM07 System Prompt Leakage)
5. **Data retention** — what does it log/store, and for how long? (LLM02 Sensitive Information Disclosure)

## Method

1. Interview the agent with the five questions above.
2. For each answer, **map the finding to its OWASP category** and note the risk.
3. Produce a findings summary (the deliverable a real security architect writes).
4. Submit → flag `THM{<redacted>}`.

## Techniques / concepts applied

- Pre-deployment AI audit / security architecture review
- OWASP LLM Top 10 classification
- Findings reporting mapped to a recognized framework

## Result

Audit completed and findings mapped; flag captured. This mirrors a real AI procurement/deployment review gate.
