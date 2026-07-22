# Notes — Understanding AI Supply Chains

## Task 2 — The Four Components
The AI supply chain adds the **trained model** over traditional software. Components:
- **Datasets** — training/eval data.
- **Dependencies** — packages/libraries.
- **Frameworks** — PyTorch, TensorFlow, Keras, scikit-learn.
- **Models** — architecture + training data + training process + serialised weights.

Pickle-based model files can **execute code at load time**. Transfer learning / fine-tuning (incl. LoRA adapters) means backdoors in a base model can survive downstream — **trust is inherited**.

## Task 3 — Two Consumption Paradigms
- **Download paradigm:** you host the weights; file format drives risk:
  - Pickle (`.pkl`/`.pt`/`.bin`) = code execution risk.
  - SafeTensors = safe (data only).
  - GGUF = no serialisation exploit, but weight/quantisation backdoor risk remains.
- **API paradigm:** only JSON crosses your boundary, but you trust the provider's hidden pipeline — training data, silent fine-tuning/updates, system prompts, multi-tenant hosting.

## Task 4 — The Four Attack Layers
- **Model** — serialisation / architecture / weights levels.
- **Dependency** — dependency confusion, typosquatting.
- **Data** — poisoning as little as ~0.1%; DoS as low as ~0.001%.
- **Infrastructure** — repo/account/CI-CD compromise.
They **compound** (multiple layers in one campaign).

## Task 5 — Real-World Incidents
| Incident | Year | Layer |
|----------|------|-------|
| SolarWinds (build-process backdoor) | 2020 | Infrastructure |
| Log4Shell | 2021 | Dependency |
| PyTorch `torchtriton` dependency confusion | 2022 | Dependency |
| Hugging Face exposed tokens / ~100 malicious models | 2023–24 | Infra / Model |
| Ultralytics (YOLO) CI/CD cryptominer | 2024 | Infrastructure |
| @solana/web3.js stolen npm creds | 2024 | Infrastructure |
| NullifAI scanner evasion (Hugging Face) | 2025 | Model |

## Task 6 — Practical (summary)
Compare a suspicious model vs. a verified baseline across organisation trust, download counts, file format (pickle vs. SafeTensors), security-scan results, and model-card quality → make a trust decision. See writeup.
