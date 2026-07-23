# TryHackMe — AI Security Threats

> Room 2 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). Where the foundations meet security: how attackers weaponize AI, what vulnerabilities models introduce, and how defenders fight back.


## Overview

The first hands-on security room. It introduces the **MITRE ATLAS** framework, the core AI model vulnerabilities, AI-enhanced attacks (deepfakes, AI phishing, AI malware), and defensive AI in the SOC. Unlike Room 1, it uses real, named industry tools and standards.

## Learning objectives

- Enumerate the core AI model vulnerabilities and map them to MITRE ATLAS
- Perform a basic prompt injection to extract a system prompt
- Recognize AI-enhanced attacks (deepfakes, AI phishing/malware) in SOC triage
- Apply defensive AI across analysis, prediction, summarization, and investigation
- Understand baseline controls for securing AI (RBAC, MFA, ISO/IEC 27090, SHAP/LIME)

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Recap + objectives |
| 2 | Vulnerabilities in AI Models | MITRE ATLAS + 5 core vulns; **prompt injection vs. MENTOR** |
| 3 | AI-Enhanced Attacks | Deepfakes, AI phishing, AI malware; SOC inbox triage |
| 4 | Defensive AI | AI co-pilot through "Incident Zero" |
| 5 | Securing AI | RBAC/MFA, ISO/IEC 27090, SHAP/LIME |
| 6 | Practical | "AI Security Analyst Orientation" capstone → flag |
| 7 | Conclusion | Recap and bridge to Room 3 |

Concept notes: [`notes.md`](./notes.md)
Walkthroughs: [`writeups/task2-mentor-prompt-injection.md`](./writeups/task2-mentor-prompt-injection.md) · [`writeups/task6-analyst-orientation.md`](./writeups/task6-analyst-orientation.md)

## Frameworks & tools introduced

- **MITRE ATLAS** — ATT&CK-style framework for adversarial ML threats
- **Microsoft Defender for Endpoint**, **Splunk** — AI-augmented analysis/detection
- **SHAP**, **LIME** — model explainability libraries used as security signals
- **ISO/IEC 27090** — standard for AI-specific security threats
- **RBAC / MFA** — access controls applied to AI systems

## Core AI model vulnerabilities (Task 2)

1. **Prompt injection** — override system instructions via crafted input
2. **Data poisoning** — corrupt training data to bias/backdoor a model
3. **Model theft / extraction** — repeated API querying to train a clone
4. **Privacy leakage** — sensitive training data resurfacing via prompting
5. **Model drift** — degradation over time, a monitoring & security signal

## Skills & mapping

`MITRE ATLAS` · `prompt injection` · `deepfake/phishing triage` · `AI-augmented SOC` · `RBAC/MFA` · `SHAP/LIME`

Strongest role mappings: **SOC analyst / incident response** (Tasks 3–4), **AI red-teamer / LLM pentester** (Task 2), **ML security engineer / MLSecOps / AI GRC** (Tasks 2 & 5).

## Reference

- MITRE ATLAS: https://atlas.mitre.org/
- IBM Cost of a Data Breach: https://www.ibm.com/reports/data-breach
