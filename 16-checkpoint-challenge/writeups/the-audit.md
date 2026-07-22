# Walkthrough — The Audit (Checkpoint challenge)

> Assess candidate models and make the production go/no-go call.
>
> **Note:** flag redacted per THM policy. Documents the decision method.

## Objective

Three of four candidate code-review models were auto-flagged unsafe. Assess Candidate A yourself, then approve exactly one candidate for production.

## Method

1. **Apply the Model Acquisition Framework to Candidate A** (`code_reviewer_pro.pkl`):
   - Static scan → `os` import + `os.system` curl beacon (code exec).
   - Behavioural telemetry → reads `/etc/passwd`, returns an `int` instead of a model.
   - Policy → driven by an external, unverified `CommunityReview` template; `security_review_flag` disabled.
   - Verdict: **Reject.**
2. **Confirm the pre-flagged three:**
   - **C** (`pr_analyzer_v3.h5`) → Lambda `exec(open('/tmp/.cache').read())` → reject.
   - **D** (`api.reviewsvc.io`) → unverified endpoint, undisclosed provenance, uninspectable vendor prompt, auto-approves → reject.
3. **Identify the safe candidate — B** (`code_reviewer_lite.safetensors`): SafeTensors (no code exec), internal verified template, guardrail enabled, produces a real review verdict ("Needs Changes").
4. **Recover the flag** via the linking element (a beacon session ID split across the telemetry summary and the agent). *(Value redacted.)*

## Decision
- Reject A, C, D. **Approve Candidate B** for production.

## Techniques / concepts applied
Multi-format risk assessment (pickle/H5/SafeTensors/API) · telemetry correlation · the 5-gate Model Acquisition Framework · production go/no-go judgement.
