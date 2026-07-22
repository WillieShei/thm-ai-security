# Notes — AI Models & Data

## Task 2 — Training Data

- **Four sourcing categories** (differing trust): web scraping, licensed datasets, synthetic data, internal corpora.
- **Common Crawl** — dominant public corpus behind GPT-3, DeepSeek, LLaMA.
- **Data provenance** — origin, collection date, modification history. The Data Provenance Initiative found widespread unspecified/miscategorized dataset licenses.
- **SBOM → ML-BOM** — extend software bill-of-materials practice (SolarWinds/EO 14028 driven) to ML assets.
- **Secrets leakage** — Truffle Security scanned Common Crawl and found ~12,000 **live** API keys/passwords. Scraped data can carry credentials straight into training.
- Tension: GDPR data minimization vs. AI's appetite for data.

## Task 3 — Building the Model

- **Epochs / training loop;** overfitting reframed as a **memorization / data-extraction** risk.
- **Validation sets** as a quality + security gate.
- **Post-training optimization:**
  - *Pruning / quantization* — shrinks models but research shows quantization can **silently degrade safety alignment** and defeat backdoor defenses only tested at full precision.
  - *Federated learning* — raw data stays local (privacy win) but **poisoned gradient updates** are hard to detect at aggregation (integrity risk).

## Task 4 — The Inheritance Problem

- **Base model vs. fine-tuning** — what fine-tuning does and doesn't change.
- **Three inheritance risks:**
  1. **Alignment erosion** — safety degraded with as few as ~10 adversarial fine-tuning examples for < $0.20 (Stanford/Princeton).
  2. **Expanded attack surface** — increased prompt-injection susceptibility after fine-tuning (Cisco).
  3. **Untracked versioning** — downstream fine-tunes silently inherit upstream backdoors/issues.

## Task 5 — The Black Box Problem

- Trained **weights are opaque** — no human-readable record of how they were shaped.
- **Sampling behavior** (benchmarks, adversarial red-teaming) ≠ **true auditing**.
- **Model cards** (Google, 2019) should document: training data, intended use, evaluation, limitations, bias assessment, license — but are voluntary and often incomplete/absent.
- A sparse/missing model card = a security warning sign.

## Task 7 — Conclusion

- The throughline: **security review must happen at every stage** of the AI build pipeline, not just at deployment — unaudited data, embedded secrets, quantization/FL trade-offs, fine-tuning inheritance, and black-box gaps compound.
