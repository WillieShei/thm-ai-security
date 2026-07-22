# Notes — Checkpoint (Challenge)

Single challenge ("The Audit"). Capstone decision for Section 4.

## Scenario
- Four candidate code-review models submitted to SupplySecLab; screening flagged three as unsafe. Assess Candidate A and pick the production model.

## Candidate telemetry
- **A** `code_reviewer_pro.pkl` → Reject: `os` import, reads `/etc/passwd`, `os.system` curl beacon, returns `int`, external `CommunityReview` template, `security_review_flag` disabled.
- **B** `code_reviewer_lite.safetensors` → Approve: SafeTensors, internal verified template, guardrail enabled, verdict "Needs Changes".
- **C** `pr_analyzer_v3.h5` → Reject: dangerous Lambda `exec(open('/tmp/.cache').read())`.
- **D** `api.reviewsvc.io` → Reject: unverified endpoint, no disclosed provenance, no compliance cert, vendor-managed uninspectable prompt, auto-approves.

## Candidate A findings (for the assessment)
- Suspicious file read: `/etc/passwd`.
- Disabled guardrail flag: `security_review_flag`.
- Policy template: external, unverified `CommunityReview` template.
- Flag-linking element: a beacon session ID split across telemetry + agent.
- Recommendation: **Reject**.

## Production decision
- Approve **Candidate B** (only safe option).

> Flag redacted per THM policy.
