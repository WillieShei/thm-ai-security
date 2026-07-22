# Notes — LLM Security

Organized by the room's four threat categories.

## Task 2 — Data-Based Threats
- **Training-data extraction:** recover verbatim training sequences via crafted prompts (GPT-2 study extracted hundreds of examples).
- **Membership inference:** determine whether a specific known sample was in the training set — the model shows higher confidence on memorized examples. *(Hands-on: identify which of three samples was a training member.)*
- **Prompt / system-prompt leakage (LLM07:2025):** e.g., the 2023 Bing "Sydney" extraction. Never treat the system prompt as a security boundary.

## Task 3 — Model-Based Threats
- **Model extraction / theft:** query a public API to build input→output pairs and train a surrogate/distilled model. Mindgard extracted ChatGPT-3.5-Turbo into a 100× smaller model for ~$50.
- **Model inversion:** reconstruct unknown training data by optimizing inputs / decoding embeddings. Distinct from membership inference. *(Hands-on: reconstruct a redacted employee ID + clearance level.)*

## Task 4 — System-Based Threats
- **Prompt injection = context-window poisoning:** once system + user + retrieved content are concatenated into one token stream, the model can't structurally tell trusted from untrusted.
- **Context overflow / unbounded consumption (LLM10:2025):** exploit the FIFO context buffer to push security instructions out of memory; "**Denial of Wallet** (DoW)" cost attacks.
- **Memory poisoning:** multi-turn manipulation of persistent conversation state (the "cat equals dog" example). *(Hands-on: perform a memory-poisoning attack for a flag.)*

## Task 5 — User-Based Threats
- **LLM-powered social engineering:** highly convincing spear-phishing, optionally combined with leaked internal data + OSINT.
- **Trust exploitation / misinformation (LLM09:2025):** **package hallucination** — the LLM recommends a non-existent package, an attacker pre-registers that name as malware ("slopsquatting"). *(Hands-on: validate AI advice, spot the malicious hallucinated package.)*

## Task 6 — Conclusion
- Ten-threat cheat-sheet mapping each threat to target/attack surface, input, and output — a reusable reference card for repeatable LLM assessments.
