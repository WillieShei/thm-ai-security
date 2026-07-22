# TryHackMe — Jailbreaking

> Room 11 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). Attacking a model's own safety alignment — why "jails" exist, why they're fragile, and the classic + multi-turn techniques that bypass them.

![Difficulty](https://img.shields.io/badge/difficulty-Medium-yellow)
![Type](https://img.shields.io/badge/type-Safety%20Red%20Team-red)
![Status](https://img.shields.io/badge/status-Completed-success)

## Overview

Where prompt injection targets the *application*, jailbreaking targets the *model's safety filters directly*. This room is strongly grounded in real AI safety research — RLHF fragility, activation-space ablation, the Crescendo attack, and the DAN phenomenon — mapping to the frontier red-teaming done at AI labs before model releases.

## Learning objectives

- Distinguish jailbreaking from prompt injection precisely
- Explain why safety alignment (RLHF) is probabilistic and fragile
- Apply classic jailbreak techniques (roleplay, emotional manipulation, obfuscation, sandwiching)
- Apply multi-turn conditioning strategies
- Understand the DAN history and its research significance

## Task index

| # | Task | What it covers | Hands-on |
|---|------|----------------|----------|
| 1 | Introduction | Framing, objectives | — |
| 2 | Prompt Injection vs Jailbreaking | Willison's distinction | — |
| 3 | Why Models Have "Jails" | RLHF, alignment fragility, alignment tax | — |
| 4 | Classic Jailbreak Techniques | Roleplay, Grandma, obfuscation, sandwiching | Submit 3 techniques |
| 5 | Multi-turn Jailbreaking | Crescendo, consistency bias, poisonous seeds | — |
| 6 | Case Study: DAN | History from Reddit origin to 2025 crackdown | — |
| 7 | Challenge | TryJailbreakMe capstone → flag | Extract a secret |
| 8 | Conclusion | Recap; bridge to Prompt Defence |

Concept notes: [`notes.md`](./notes.md)
Walkthrough: [`writeups/task7-tryjailbreakme.md`](./writeups/task7-tryjailbreakme.md)

## Jailbreaking vs. prompt injection (Task 2)

Per Simon Willison: **prompt injection** requires concatenating trusted + untrusted strings (an app-integration attack); **jailbreaking** targets the model's own safety filters directly, no concatenation required. Precise classification matters for accurate reporting.

## Why alignment is fragile (Task 3)

- RLHF = probabilistic pattern-learning, **not** enforced rule-following.
- Activation-space **ablation** can remove specific safety "directions."
- Fine-tuning on just **1,000 benign samples** can degrade safety by **60%+** (reinforces Room 3's inheritance problem).
- Helpfulness–harmlessness paradox / "alignment tax"; Safe RLHF (dual reward models).
- Willison: "you cannot use a language model to perfectly filter the output of the same language model."

## Classic techniques + cited success rates (Task 4)

- **Roleplay/persona** — 87.3% (open-source), 84.3% (commercial); fiction-writer & authority personas best
- **"Grandma exploit"** — emotional + fictional framing; 92% for emotional appeals; advanced models *more* susceptible
- **Obfuscation/encoding** — Base64, leetspeak, low-resource languages (Zulu, Swahili, Gaelic), token-boundary word fragmentation
- **Instruction sandwiching** — bury the harmful request among benign tasks

## Multi-turn strategies (Task 5)

Consistency bias (+10–20% vs. single-turn) · trust-building (foot-in-the-door) · gradual escalation (**Crescendo**, 89%) · context shaping ("poisonous seeds") · trigger phrases · backtracking/adaptation.

## Skills & mapping

`safety/alignment red-teaming` · `persona & emotional attacks` · `obfuscation/encoding` · `multi-turn conditioning` · `precise classification`

Primary role: **AI safety / alignment red-teamer** (frontier-model testing). Secondary: **AI security researcher / threat intelligence** (DAN sociotechnical context).

## Reference

- Wei et al., "Jailbroken: How Does LLM Safety Training Fail?": https://arxiv.org/abs/2307.02483
- Crescendo attack: https://crescendo-the-multiturn-jailbreak.github.io/
- MITRE ATLAS: https://atlas.mitre.org/
