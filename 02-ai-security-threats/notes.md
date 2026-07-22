# Notes — AI Security Threats

## Task 2 — Vulnerabilities in AI Models

- **MITRE ATLAS** — an ATT&CK-style knowledge base of adversary tactics/techniques specific to AI/ML systems. Use it the way a SOC uses ATT&CK.
- **Five core vulnerabilities:**
  - **Prompt injection** — attacker input overrides the system prompt.
  - **Data poisoning** — malicious training data biases or backdoors the model.
  - **Model theft / extraction** — repeatedly query an API to reconstruct/clone the model.
  - **Privacy leakage** — sensitive training data resurfaces through prompting.
  - **Model drift** — model behavior degrades over time; relevant to both quality and security.
- Hands-on: extract the system prompt from simulated chatbot **MENTOR** via prompt injection.

## Task 3 — AI-Enhanced Attacks

- **AI-generated malware** — lowers the skill barrier to writing malicious code.
- **Deepfakes** — voice/video impersonation for fraud (fake wire-transfer calls, fake job interviews).
- **AI-enhanced phishing** — fluent, targeted phishing at scale; guardrail bypass via prompt injection means "broken English" is no longer a reliable tell.
- Hands-on: triage a simulated SOC inbox and identify the specific AI enhancement behind each item.

## Task 4 — Defensive AI

- **Business case:** IBM Cost of a Data Breach — AI-assisted security yields cost savings and ~108-day faster breach containment.
- **Four defensive use cases:**
  - *Analysis* — anomaly detection in logs/traffic (Splunk, Microsoft Defender for Endpoint).
  - *Prediction* — proactive phishing detection & automated blocking.
  - *Summarization* — LLM incident/threat-intel summaries.
  - *Investigation* — LLM-assisted log analysis, query suggestion, threat hunting.
- Hands-on: **"Incident Zero"** — drive an AI co-pilot through analyze → triage → summarize → hunt.

## Task 5 — Securing AI

- Only **24%** of generative AI initiatives are currently secured (IBM).
- **Access control:** RBAC + MFA to restrict who/what can interact with the model.
- **Data privacy:** audit, minimize, encrypt sensitive training data.
- **Standard:** **ISO/IEC 27090** — identifying/mitigating AI-specific security threats.
- **Monitoring / explainability:** **SHAP** and **LIME** interpret model behavior; anomalous/drifted output becomes a security signal (not just a performance issue).

## Task 7 — Conclusion

- Full offense/defense picture. Next rooms drill into how each attack works, how to test for it, and how to defend properly.
