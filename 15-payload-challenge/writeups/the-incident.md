# Walkthrough — The Incident (Payload challenge)

> Single-VM incident investigation. Applies every Section 4 technique.
>
> **Note:** live-VM challenge — exact flag and instance-specific values are redacted per THM policy. Documents the method that answers the seven questions.

## Objective

A production code-review model is phoning home. Investigate `/opt/supply-chain/incident/`, determine what happened, and recover the campaign flag.

## Method

1. **Establish the timeline.**
   ```bash
   cat logs/deployment.log
   ```
   Identify the replacement model's org and the gap (days) between deployment and the SOC alert.
2. **Examine the running production model.**
   ```bash
   fickling --check-safety -p production_model.pkl
   ```
   Confirm the code-exec path and identify the function the payload uses to run the shell command (`os.system`) and the command that captures host identity (`hostname`).
3. **Read the beacon evidence.**
   ```bash
   cat beacon_capture.log
   ```
   Note the HTTP method of the outbound beacon.
4. **Assess the staged candidate.**
   ```bash
   python3 inspect_h5_model.py candidate_model.h5
   ```
   Find the suspicious (disguised Lambda) layer name.
5. **Recover the split flag** — combine the piece in `beacon_capture.log` with the piece in the candidate model to reconstruct the campaign ID.

## The seven questions (method, not answers)
1. Replacement model's org name → `deployment.log`.
2. Days between deployment and SOC alert → log timeline.
3. Function the payload uses to run the shell command → decompile → `os.system`.
4. Shell command capturing host identity → `hostname`.
5. HTTP method in the outbound beacon → `beacon_capture.log`.
6. Suspicious layer name in `candidate_model.h5` → `inspect_h5_model.py`.
7. Final flag → split across `beacon_capture.log` + candidate model.

## Techniques / concepts applied
Incident timeline reconstruction · static pickle analysis (Fickling) · beacon/log analysis · Keras architecture inspection · multi-artefact flag recovery.
