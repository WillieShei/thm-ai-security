# TryHackMe — Prompt Engineering

> Room 4 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). The practical mechanics of controlling LLMs: tokens, generation parameters, prompt structure, the system/user instruction hierarchy, and advanced techniques.

![Difficulty](https://img.shields.io/badge/difficulty-Easy-brightgreen)
![Type](https://img.shields.io/badge/type-LLM%20Control-blue)
![Status](https://img.shields.io/badge/status-Completed-success)

## Overview

Shifts from architecture/data concerns to *how you actually drive an LLM*. The security throughline is the **system/user instruction hierarchy** and its fragility — the conceptual basis for prompt injection, built on in later rooms.

## Learning objectives

- Explain tokenization and LLM nondeterminism (and why it matters for security testing)
- Tune generation parameters: temperature, max tokens, top-p
- Construct prompts using the four pillars
- Understand the system vs. user prompt hierarchy and its limits
- Apply few-shot and Chain-of-Thought techniques to security tasks

## Task index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Tokens, parameters, four pillars |
| 2 | LLM Fundamentals | Tokenization, nondeterminism, temperature/top-p/max tokens |
| 3 | The Anatomy of a Prompt | Four pillars: instruction, context, format, constraints |
| 4 | System vs. User Prompts | Instruction hierarchy + its probabilistic limit |
| 5 | Advanced Prompting Techniques | Shot spectrum, Chain-of-Thought, templates |
| 6 | Challenge | PromptSec graded exercise — 40 pts → flag |
| 7 | Conclusion | Recap; bridge to AI Forensics |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/task6-promptsec-challenge.md`](./writeups/task6-promptsec-challenge.md)

## Key concepts

- **Tokenization:** tokens ≈ 3–4 chars; scheme-specific (GPT BPE vs. BERT WordPiece). Affects cost and context budgeting.
- **Nondeterminism:** a security-relevant property — a defense that works once may fail on retry, so adversarial testing must be **probabilistic**, not one-shot.
- **Generation parameters:** temperature (randomness), max tokens (length/cost ceiling), top-p/nucleus sampling (don't combine with temperature), context window (working memory).
- **Four pillars of a prompt:** instruction/task, context, output format, constraints.
- **System vs. user hierarchy:** LLMs process all input as one undifferentiated token stream, so the hierarchy is a *training convention*, not a hard boundary → the root of prompt injection.
- **Advanced techniques:** zero/one/few-shot (in-context learning), Chain-of-Thought ("Let's think step by step", effective ~>100B params, basis of o1/extended thinking), reusable prompt templates.

## Skills & mapping

`tokenization` · `parameter tuning` · `prompt design` · `instruction hierarchy` · `few-shot / CoT`

Role mappings: **prompt engineer / AI app developer** (parameters, four pillars, templates), **AI red-teamer / LLM pentester** (instruction hierarchy fragility), **AI-augmented SOC analyst** (CoT for log/incident triage).

## Reference

- OWASP Top 10 for LLM Applications: https://genai.owasp.org/
- Chain-of-Thought prompting: https://arxiv.org/abs/2201.11903
