# Walkthroughs — LLM Security Hands-On Attacks

> One live attack per threat category, all against a simulated chatbot.
>
> **Note:** flags and exact payloads redacted per THM policy. These document approach and reasoning.

---

## Task 2 — Membership Inference Attack

**Goal:** determine which of three placeholder samples was part of the model's training data.

**Approach:**
1. Present each candidate sample to the model and observe its **confidence / fluency / willingness to complete** it.
2. A training *member* typically triggers higher confidence or near-verbatim continuation (memorization signal).
3. Compare the three, pick the one with the strongest memorization signal → flag `THM{<redacted>}`.

**Concept:** membership inference exploits the confidence gap between memorized (seen) and novel (unseen) data.

---

## Task 3 — Model Inversion Attack

**Goal:** reconstruct a redacted piece of training data (an employee ID and clearance level).

**Approach:**
1. Probe the model with prompts that coax it to *complete* or *reveal* the redacted attributes rather than asking directly.
2. Iterate — narrow the reconstruction using partial disclosures, decoding what the model has effectively memorized.
3. Assemble the reconstructed value → flag `THM{<redacted>}`.

**Concept:** distinct from membership inference — here you rebuild *unknown* data, not confirm a *known* sample.

---

## Task 4 — Memory Poisoning Attack

**Goal:** manipulate the chatbot's persistent conversation state to bend later behavior.

**Approach:**
1. Over multiple turns, seed false "facts" the model will carry forward (the "cat equals dog" pattern).
2. Reinforce the poisoned state so it persists in context.
3. Trigger the behavior that depends on the poisoned memory → flag `THM{<redacted>}`.

**Concept:** stateful conversational systems trust their own history; poison the history, poison the output.

---

## Task 5 — Package Hallucination / Slopsquatting

**Goal:** validate the LLM's coding advice and identify the malicious recommended package.

**Approach:**
1. Take the model's package recommendation and **verify it** against a real registry rather than trusting it.
2. Spot the non-existent / suspicious package name an attacker would pre-register as malware.
3. Flag the malicious recommendation → flag `THM{<redacted>}`.

**Concept:** "slopsquatting" — attackers register package names LLMs are known to hallucinate, so trusting AI output installs malware. Always verify before `pip install`.

---

## Techniques / concepts applied
Model privacy attacks (membership inference, model inversion) · model extraction awareness · stateful memory poisoning · AI-supply-chain verification · critical validation of AI output.
