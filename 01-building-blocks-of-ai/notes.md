# Notes — The Building Blocks of AI

Per-task concept notes. Written for revision, not as answer keys.

## Task 2 — What is AI and Machine Learning?

- **AI** is the broad field; **machine learning** is the subset where systems learn patterns from data rather than being explicitly programmed.
- **The ML lifecycle:**
  1. Problem definition
  2. Data collection & cleaning
  3. Training
  4. Evaluation & tuning
  5. Deployment
  6. Monitoring & retraining
- **Overfitting:** a model that memorizes its training data instead of generalizing. Introduced here as a quality issue; revisited later as a *security* issue (memorized data can be extracted).
- Interactive agent **ARIA** — you fix a broken ML lifecycle by placing the stages in the right order.

## Task 3 — Machine Learning Algorithms

- **Algorithmic loop:** decision process → error function → optimization (repeat).
- **Four paradigms:**
  - *Supervised* — labeled data (e.g., spam classification).
  - *Unsupervised* — unlabeled data, find structure (e.g., **anomaly detection in network traffic** → IDS/SOC relevance).
  - *Semi-supervised* — mix of labeled/unlabeled.
  - *Reinforcement learning* — reward-driven (e.g., autonomous systems).
- Exercise: match algorithm type to a "mission" scenario.

## Task 4 — Neural Networks and Deep Learning

- **Neuron/synapse analogy;** architecture = input layer → hidden layer(s) → output layer, connected by **weights**.
- **Depth** enables automatic **feature extraction**; "deep" = more than three layers.
- Deep learning differs from classic ML by not requiring hand-labeled features.
- Hands-on: manually operate the simulated network **NEURON-1** through input → hidden → output.

## Task 5 — Large Language Models

- **Pre-training:** next-word prediction over huge corpora; behavior encoded in **parameters**.
- **Backpropagation:** how the network adjusts weights from error.
- **Transformer + attention:** the model weighs which tokens matter for context — the "bank" (river vs. money) / "loan" disambiguation example.
- **GPU parallelism** makes training at scale feasible.
- **RLHF (Reinforcement Learning from Human Feedback):** the alignment/fine-tuning step that shapes a raw next-word predictor into a helpful, safer assistant. *Remember this — the Jailbreaking room attacks exactly this alignment.*

## Task 7 — Conclusion

- Synthesizes the stack: **AI ⊃ ML ⊃ Deep Learning ⊃ LLMs**.
- Explicitly sets up Room 2: how attackers weaponize these technologies, what vulnerabilities models introduce, and how defenders respond.
