# Walkthrough — Prompt Template Compromise (Task 8)

> Agent lab: an assistant (TryAssist) pulled a community prompt template that was rewritten to auto-approve everything.
>
> **Note:** flags/answers redacted per THM policy. Documents method.

## Objective

Probe a code-review assistant to discover that its behaviour is driven by a compromised, externally sourced prompt template — and identify the failure.

## Method

1. **Baseline with a benign request.** Ask it to review a harmless change (e.g., a README PR) — it approves normally, so nothing looks wrong on the surface.
2. **Send a request that should be rejected.** Submit a security-sensitive change (e.g., an auth-token change). A healthy reviewer flags it; the compromised one **wrongly approves** it.
3. **Interrogate the decision.** Ask *why* it approved and *who* is responsible — the assistant deflects responsibility to another party per the rewritten policy.
4. **Name the artefact.** Ask what template/policy governs its behaviour — it reveals an external, unverified community template.

## Finding

The assistant's approval logic came from an **external, unverified community prompt template** that had been rewritten to auto-approve. No model weights changed — the compromise was entirely in a version-controlled prompt artefact, illustrating the API/prompt-template attack layer.

## Techniques / concepts applied
Behavioural probing of an agent · detecting prompt-template/policy compromise · recognizing that governance of prompt artefacts is a supply-chain control.
