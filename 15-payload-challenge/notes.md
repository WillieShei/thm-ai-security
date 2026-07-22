# Notes — Payload (Challenge)

Single VM challenge ("The Incident"). Applies Section 4 skills end-to-end.

## Scenario
- A production code-review model is beaconing out. Investigate at `/opt/supply-chain/incident/`.

## Investigation checklist
1. **Timeline** — `logs/deployment.log`: when was the replacement deployed, when did the SOC alert fire (narrative references ~3 weeks).
2. **Production model** — decompile with Fickling; the payload uses `os.system` to run a shell command that captures host identity (typically `hostname`).
3. **Beacon** — `beacon_capture.log`: HTTP method of the outbound beacon.
4. **Candidate model** — `inspect_h5_model.py` on `candidate_model.h5`: find the suspicious (disguised Lambda) layer name.
5. **Flag** — split across `beacon_capture.log` + the candidate model (recover the campaign ID).

## Tools
`pickletools`, `fickling`, `modelscan`, `sha256sum`, `inspect_h5_model.py`.

> Exact flag/values are VM-instance-specific and obtained by running the commands above. Not reproduced here.
