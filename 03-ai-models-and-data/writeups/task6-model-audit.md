# Walkthrough — Model Repository Audit (Task 6)

> Hands-on due-diligence exercise: audit a simulated Hugging Face-style model repository and find the hidden red flags.
>
> **Note:** flag redacted per THM policy. Documents method and reasoning.

## Objective

Review a model's card, metadata, file listing, and training details; identify the supply-chain red flags; and receive feedback on the severity of each finding. Correctly completing the audit yields the flag.

## Environment

- Simulated model repository resembling a Hugging Face model page: model card, files/versions tab, metadata, training description.

## Approach — audit checklist

1. **Model card completeness.** Is training data documented? Intended use? Evaluation results? Known limitations? Bias assessment? License? Missing sections are themselves findings (Task 5).
2. **Provenance & licensing.** Does the stated data source match the license? Look for unspecified or contradictory dataset licensing (Task 2).
3. **Secrets / sensitive data.** Check file listings and training details for leaked keys, credentials, or PII embedded from scraped data (Truffle Security / Common Crawl lesson).
4. **Base-model lineage.** Is the base model and version tracked? An untracked or vague base model means inherited backdoors can't be reasoned about (Task 4).
5. **Optimization disclosures.** Any mention of quantization/pruning without safety re-evaluation? That's a silent-alignment-degradation risk (Task 3).
6. **Rank findings by severity** and submit → flag `THM{<redacted>}`.

## Techniques / concepts applied

- Model-card auditing vs. behavioral sampling
- Supply-chain / metadata red-flag inspection (analogous to npm/PyPI package audits)
- ML-BOM thinking: treat the model as a dependency with a bill of materials

## Role relevance

Direct analogue of a **third-party model risk review** — the gatekeeping step before a model is approved for production in an enterprise GRC/security workflow.

## Result

Red flags identified and severity-rated; flag captured.
