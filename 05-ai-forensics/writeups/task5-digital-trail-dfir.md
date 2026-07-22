# Walkthrough — The Digital Trail (Task 5, RobbCo DFIR case)

> Full command-line DFIR investigation on a deployed lab machine. ML-assisted triage + manual validation to reconstruct a complete breach.
>
> **Note:** flags, hostnames, IPs, and exact artifact values redacted per THM policy. This documents the investigative methodology and the reconstructed attack chain.

## Objective

Using ML-assisted forensic scripts plus manual analysis, investigate a compromised Linux host and reconstruct the full attack chain from initial access to data exfiltration; answer the case questions to obtain the flag.

## Environment & setup

- Start the **AttackBox** and the dedicated **lab machine**.
- Activate the provided **Python virtual environment** (keeps tooling isolated — an evidence-handling good practice).
- Provided scikit-learn scripts:
  - `classify_logs.py` — classifies/triages `auth.log` entries.
  - `file_anomalies.py` — flags suspicious files on disk.

## Methodology

1. **Triage with ML, then validate manually.** Run the scripts to narrow the field, but treat every flag as a lead, not a verdict — the room deliberately includes a **false positive** (proprietary source code flagged suspicious).
2. **Auth log analysis.** Parse `auth.log` for anomalous logins, new keys, and privilege changes; correlate timestamps to build a timeline.
3. **Artifact validation.** For each flagged file, inspect it directly (file type, contents, embedded macros, encoding) before drawing conclusions.
4. **Correlate into a single narrative** across log, filesystem, and network evidence.

## Reconstructed attack chain

1. **Initial access — phishing.** A malicious macro-laden `.ods` document (`invoice_Q1_2075.ods`) delivered via phishing.
2. **Credential/SSH-key harvesting** and exfiltration once the macro executed.
3. **Remote access — dropper + reverse shell.**
4. **Privilege escalation** via an attacker-planted key in a privileged user's `authorized_keys`.
5. **Persistence** — a reverse shell disguised as a legitimate monitoring binary, backed by a **fabricated log** to blend in (anti-forensics).
6. **Exfiltration — source-code theft** via a base64-encoded, compressed archive staged in shared memory (`/dev/shm`), decoded/unpacked with standard tools (`base64`, `tar`).

## Techniques / concepts applied

- ML-assisted log/file triage (scikit-learn) + human-in-the-loop validation
- `auth.log` forensics, SSH-key privilege-escalation detection
- Macro-based malware / phishing forensics
- Detecting disguised binaries and fabricated supporting logs (threat hunting)
- Artifact decoding (`base64`, `tar`); timeline reconstruction

## Lessons

- The AI's **false positive** (legit source code flagged) is the point: AI accelerates triage but cannot be trusted blind — every finding needs human confirmation for a legally defensible investigation.

## Result

Full chain reconstructed; case questions answered; flag captured.
