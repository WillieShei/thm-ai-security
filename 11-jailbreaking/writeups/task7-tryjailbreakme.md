# Walkthrough — TryJailbreakMe (Task 7)

> Capstone: combine the room's techniques to make a chatbot reveal a secret it was instructed never to disclose.
>
> **Note:** flag and exact prompts redacted per THM policy. Documents technique selection and reasoning — no working jailbreak strings.

## Objective

Convince a guarded chatbot to reveal a secret flag, applying the jailbreak techniques from Tasks 4–5 individually or in combination.

## Approach — layered technique selection

1. **Recon the refusal.** Probe normally to see *how* it refuses (does it refuse the topic, or specific phrasing?). That tells you which technique class fits.
2. **Try a persona/roleplay frame.** Recast the request inside fiction or an authority context where disclosure seems in-character (highest cited success rate).
3. **Add emotional/contextual framing** if roleplay alone stalls (the "Grandma"-style approach).
4. **Obfuscate the trigger** if a keyword filter blocks you — encoding or rephrasing to slip past surface-level pattern matching.
5. **Go multi-turn.** If single-shot fails, build trust over turns and **escalate gradually** (Crescendo pattern), using the model's own prior cooperative outputs as leverage (consistency bias).
6. **Backtrack and adapt** on refusal — change the frame rather than repeating the same payload.
7. Extract the secret → flag `THM{<redacted>}`.

## Techniques / concepts applied
Roleplay/persona · emotional framing · obfuscation/encoding · instruction sandwiching · multi-turn conditioning (trust-building, gradual escalation, backtracking).

## Why this mirrors real work
This is exactly the structure of frontier-model safety red-teaming done before releases at major AI labs — probing alignment with layered, adaptive techniques and documenting what succeeds, so the model can be hardened.

## Result
Secret extracted; flag captured. Path complete → next module focus is **Prompt Defence** (mitigations).
