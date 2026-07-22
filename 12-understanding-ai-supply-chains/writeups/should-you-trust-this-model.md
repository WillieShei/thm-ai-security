# Walkthrough — "Should You Trust This Model?" (Task 6)

> Model-vetting practical: compare a suspicious model against a verified baseline and decide whether to use it.
>
> **Note:** flags and instance-specific answer values are redacted per THM policy. This documents the vetting methodology.

## Objective

Given a suspicious model and a verified baseline, evaluate trust signals and decide: use it or reject it.

## Vetting checklist

| Signal | What to check |
|--------|---------------|
| **Organisation** | Verified badge? Account age? Number of models published? A brand-new org with one model and a trustworthy-sounding name is a red flag. |
| **Popularity** | Download counts — a legitimate baseline has orders of magnitude more. |
| **File format** | Pickle (`pytorch_model.bin`) = code-exec risk; SafeTensors (`model.safetensors`) = safe. Prefer SafeTensors. |
| **Security scan** | Critical findings (e.g., `os` import + `__reduce__`/`subprocess.Popen`) = reject. |
| **Model card** | Thorough (training data, limitations, benchmark results like GLUE) vs. sparse/vague. |

## Method

1. Line up suspicious vs. baseline across every signal above.
2. Any single critical scan finding (system-command execution via pickle) is disqualifying on its own.
3. Combine signals: unverified new org + tiny download count + pickle format + critical scan + vague card → **Reject**.

## Outcome

Verdict: **reject the suspicious model**, prefer the verified SafeTensors baseline. (Specific answer values are instance-specific and omitted here.)

## Techniques / concepts applied
Model provenance evaluation · file-format risk triage · security-scan interpretation · model-card review.
