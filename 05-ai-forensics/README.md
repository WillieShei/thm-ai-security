# TryHackMe — AI Forensics

> Room 5 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). Applying AI/ML to **DFIR** — anomaly detection, deepfake/media forensics, NLP phishing analysis, and a full command-line breach investigation using scikit-learn scripts.


## Overview

The most hands-on, tool-heavy room in the path. It culminates in a real CLI DFIR investigation on a deployed lab machine (the **RobbCo / "Digital Trail"** case), reconstructing a full attack chain from phishing to exfiltration with ML-assisted triage scripts — and demonstrating why **human-in-the-loop validation** is non-negotiable.

## Learning objectives

- Map AI/ML techniques to DFIR: anomaly detection, media forensics, NLP, timeline reconstruction
- Understand precision/recall/accuracy trade-offs and the GIGO principle in evidentiary tooling
- Weigh legal/ethical constraints (Daubert admissibility, chain of custody, bias, GDPR)
- Run ML-assisted forensic scripts and validate their output against real artifacts

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | AI-for-DFIR framing, prerequisites |
| 2 | The AI Forensics Landscape | Real tool stack, precision/recall, GIGO |
| 3 | AI & DFIR | CNNs, GANs, NLP (BERT/RoBERTa), timeline reconstruction, STAMINA |
| 4 | AI Legal & Ethical Implications | Daubert, chain of custody, bias, GDPR |
| 5 | Practical: The Digital Trail | Full CLI DFIR lab → flag |
| 6 | Conclusion | "AI is not a replacement for human insight" |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/task5-digital-trail-dfir.md`](./writeups/task5-digital-trail-dfir.md)

## Real tools / techniques referenced

- **UEBA / anomaly detection:** Splunk UEBA, Elastic ML, Exabeam (Isolation Forests, Autoencoders)
- **Phishing / NLP:** Microsoft Defender for O365, Splunk NLP (BERT, RoBERTa)
- **Malware / file classification:** Microsoft Defender STAMINA, Cylance, VirusTotal ML
- **Alert triage:** Cortex XSOAR/XSIAM, IBM QRadar Advisor, CrowdStrike Falcon + Charlotte AI
- **Timeline / correlation:** Timesketch, Velociraptor, Jupyter
- **Lab tooling:** scikit-learn scripts (`classify_logs.py`, `file_anomalies.py`) against `auth.log` and the filesystem

## Legal & ethical anchors (Task 4)

- **Daubert test** — admissibility of AI-derived evidence; black-box models excluded when reasoning can't be explained
- **Chain of custody** — broken when opaque/cloud LLMs process evidence without logging
- **Bias** — facial recognition misID of minorities → documented wrongful arrests
- **Privacy** — GDPR; federated learning / on-prem processing as mitigations

## Skills & mapping

`ML-assisted triage` · `auth.log analysis` · `attack-chain reconstruction` · `macro-malware analysis` · `Linux forensics` · `human-in-the-loop validation`

Primary role: **DFIR analyst / incident responder**. Secondary: **forensic expert witness / legal-tech consultant**, **ML-assisted security tooling developer**.

## Reference

- MITRE ATLAS: https://atlas.mitre.org/
- scikit-learn: https://scikit-learn.org/
- Timesketch: https://timesketch.org/
