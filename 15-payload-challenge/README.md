# Room 15 — Payload (Challenge)

> Section 4 (AI Supply Chain Security), Room 4 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity). A single hands-on VM challenge — "The Incident."

![Difficulty](https://img.shields.io/badge/difficulty-Easy-brightgreen)
![Type](https://img.shields.io/badge/type-Challenge-lightgrey)

## Overview

A production code-review model is phoning home. Investigate the incident at `/opt/supply-chain/incident/`, establish a timeline, examine the running production model, and assess the staged candidate — applying every technique from Section 4.

## Available tooling

`pickletools` · `fickling` · `modelscan` · `sha256sum` · `inspect_h5_model.py`

## Methodology

1. **Build a timeline** from `logs/deployment.log` (deployment → SOC alert).
2. **Examine the running production model** — statically scan the pickle payload with Fickling; identify the function used to run the shell command and the host-identity capture.
3. **Read the beacon evidence** from `beacon_capture.log` (HTTP method, outbound pattern).
4. **Assess the staged candidate** `.h5` — inspect the architecture for a suspicious Lambda layer with `inspect_h5_model.py`.
5. **Recover the split flag** — pieces span `beacon_capture.log` and the candidate model.

Full method: [`writeups/the-incident.md`](./writeups/the-incident.md)
Concept recap: [`notes.md`](./notes.md)

## Skills demonstrated

`incident timeline reconstruction` · `static pickle analysis` · `beacon/log analysis` · `Keras architecture inspection` · end-to-end supply-chain triage.

> **Note:** this is a live-VM challenge; exact flag values are instance-specific and are **not** included here (redacted per THM policy). The writeup documents the investigative method.
