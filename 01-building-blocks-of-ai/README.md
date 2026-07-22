# TryHackMe — The Building Blocks of AI

> Room 1 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). Foundational concepts for everything that follows: how AI, machine learning, deep learning, and LLMs actually work.

![Difficulty](https://img.shields.io/badge/difficulty-Easy-brightgreen)
![Type](https://img.shields.io/badge/type-Foundations-blue)
![Status](https://img.shields.io/badge/status-Completed-success)

## Overview

This room builds the conceptual stack — **AI → ML → Deep Learning → LLMs** — that the rest of the path attacks and defends. It is deliberately non-tooling: no Burp, no Splunk, no Python libraries. The goal is to understand how models are built before learning how they break.

## Learning objectives

- Define AI and machine learning, and walk the full ML lifecycle
- Distinguish the four ML paradigms and match them to real problems
- Explain neural network architecture and what makes a network "deep"
- Describe how LLMs are pre-trained, and the role of transformers, attention, and RLHF

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Scope, prerequisites, objectives |
| 2 | What is AI and Machine Learning? | ML lifecycle, overfitting (agent: ARIA) |
| 3 | Machine Learning Algorithms | Algorithmic loop, 4 ML paradigms |
| 4 | Neural Networks and Deep Learning | Architecture, depth, feature extraction (NEURON-1) |
| 5 | Large Language Models | Pre-training, transformers, attention, RLHF |
| 6 | Practical | NEURON-1 CTF-style challenge → flag |
| 7 | Conclusion | Recap and bridge to Room 2 |

Full concept notes: [`notes.md`](./notes.md)
Practical walkthrough: [`writeups/task6-neuron-1-practical.md`](./writeups/task6-neuron-1-practical.md)

## Key concepts

- **ML lifecycle:** problem definition → data collection/cleaning → training → evaluation/tuning → deployment → monitoring/retraining. Overfitting is introduced here and later tied to memorization/security risk.
- **Four ML paradigms:** supervised, unsupervised, semi-supervised, reinforcement learning — with security-relevant examples (unsupervised anomaly detection in network traffic maps directly to IDS/SOC work).
- **Neural networks:** neuron/synapse analogy, input/hidden/output layers, weights, feature extraction through depth; "deep" = more than three layers.
- **LLMs:** next-word-prediction pre-training, backpropagation, transformer architecture, the attention mechanism (the "bank/loan" disambiguation example), GPU parallelism, and **RLHF** as the alignment step. Understanding RLHF here is the prerequisite for the jailbreaking room later.

## Skills & mapping

`ML lifecycle` · `neural network architecture` · `transformers/attention` · `RLHF`

Foundational for downstream roles the path targets: **AI red-teamer**, **ML security engineer**, **AI risk/governance analyst**. You can't attack attention or RLHF without first understanding them.

## Reference

- TryHackMe AI Security path: https://tryhackme.com/aisecurity
- Attention Is All You Need (transformers): https://arxiv.org/abs/1706.03762
