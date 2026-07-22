# Notes — AI Forensics

## Task 2 — The AI Forensics Landscape

- **Three ways AI aids DFIR:** parallelized data processing (deep learning/transformers), anomaly detection (supervised/unsupervised), scalability across cloud/distributed environments.
- **Real tool map:** Splunk UEBA, Elastic ML, Exabeam (Isolation Forests, Autoencoders); Defender for O365, Splunk NLP (BERT/RoBERTa); Defender STAMINA, Cylance, VirusTotal ML; Cortex XSOAR/XSIAM, QRadar Advisor, CrowdStrike Falcon + Charlotte AI; Timesketch, Velociraptor, Jupyter.
- **Limits:** probabilistic vs. deterministic behavior; the **accuracy/precision/recall** triad (matters with imbalanced datasets); overfitting hurts forensic accuracy; **GIGO** (garbage in, garbage out).

## Task 3 — AI & DFIR

- **Image/video forensics:** CNNs; ELA+CNN forgery detection (2024 study, 94% accuracy); deepfake detection.
- **GANs:** dual use — generate *and* detect deepfakes.
- **NLP:** BERT/RoBERTa for phishing detection (99% cited) and sentiment analysis.
- **Timeline reconstruction:** correlate logs, filesystem timestamps, network records; detect "impossible logins."
- **Malware:** deep-learning file representation (STAMINA); API-call-sequence-to-image classification.

## Task 4 — Legal & Ethical Implications

- **Explainability / admissibility:** black-box AI evidence excluded under the **Daubert test** when the model's reasoning can't be explained.
- **Bias / fairness:** facial recognition misidentifies Black/minority individuals at higher rates → documented wrongful arrests.
- **Accountability / chain of custody:** cloud LLM summarizing phone data broke chain-of-custody logging.
- **Privacy:** GDPR, public-cloud evidence exposure; mitigations = federated learning, on-prem/offline processing.

## Task 5 — Practical: The Digital Trail (summary)

Full CLI DFIR case (RobbCo). ML scripts (`classify_logs.py`, `file_anomalies.py`, scikit-learn) triage `auth.log` and flag files; you then **manually validate** each artifact and reconstruct the chain:

1. Phishing email → malicious macro-laden `.ods` (`invoice_Q1_2075.ods`)
2. Credential / SSH-key harvesting and exfiltration
3. Dropper + reverse shell for remote access
4. Privilege escalation via planted key in a privileged user's `authorized_keys`
5. Persistence: reverse shell disguised as a legit monitoring binary + fabricated supporting log
6. Source-code theft: base64-encoded, compressed archive staged in `/dev/shm`

Key lesson: the AI **misclassified** proprietary source code as suspicious → reinforces human-in-the-loop validation.

## Task 6 — Conclusion

- Central thesis: **AI is not a replacement for human insight** — it accelerates triage, but findings must be validated for accuracy and legal defensibility.
