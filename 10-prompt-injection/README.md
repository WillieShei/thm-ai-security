# TryHackMe — Prompt Injection

> Room 10 of the [TryHackMe AI Security path](https://tryhackme.com/aisecurity) (AI1). The deepest, most incident-rich treatment of prompt injection — direct and indirect — with two hands-on exploits.


## Overview

OWASP's **#1 LLM vulnerability**, given full technical grounding. Covers how context windows and provider formats (ChatML, Harmony) work, why the instruction boundary is only a convention, and both **direct** and **indirect** injection — the latter framed as "generative AI's greatest security flaw." Two live exploits: a $1 car purchase and a CEO-email leak via a poisoned calendar event.

## Learning objectives

- Explain the context window's five component types and provider separation formats
- Define prompt injection and its root cause (the SQL-injection analogy)
- Apply advanced direct-injection techniques beyond "ignore previous instructions"
- Exploit indirect prompt injection through ingested untrusted content

## Task index

| # | Task | What it covers | Hands-on |
|---|------|----------------|----------|
| 1 | Introduction | Terminology, objectives | — |
| 2 | How LLMs Follow Instructions | Context window, ChatML, Harmony hierarchy | — |
| 3 | What is Prompt Injection? | OWASP #1; SQL-injection analogy | — |
| 4 | Prompt Injection in Action | Real incidents + 4 direct techniques | $1 "LLMborghini" purchase |
| 5 | Indirect Prompt Injection | 4 ingestion vectors, zero-click | — |
| 6 | Practical | CalBot indirect injection | Leak CEO email via calendar event |
| 7 | Conclusion | Recap; bridge to Jailbreaking |

Concept notes: [`notes.md`](./notes.md)
Walkthroughs: [`writeups/`](./writeups/)

## Direct injection techniques (Task 4)

- **Synonym/paraphrase overrides** — defeat keyword blocklists via semantic equivalence (résumé-screening bypass)
- **Format-based injection** — hide instructions in HTML/markup/YAML (GitHub Copilot via hidden HTML tag in an issue)
- **Simulated dialogue injection** — forge fake conversation history so the model completes a "leaked" response
- **Multi-turn prompt shaping** — plant dormant instructions that activate later

## Indirect injection vectors (Task 5)

- **Web pages** — Bing Chat browser-extension attack via invisible font-size-0 text (pirate-persona phishing)
- **Emails/documents** — **EchoLeak** zero-click against Microsoft 365 Copilot
- **LLM agents/tools** — Cursor AI RCE via a shared Google Doc
- **RAG systems** — (covered further in the Data Poisoning module)

Consequences: unauthorized actions, data leaks, content manipulation, zero-click exploits.

## Named incidents referenced

Bing "Sydney" (Kevin Liu) · remoteli.io Twitter bot · $1 Chevrolet Tahoe · GitHub Copilot HTML injection · Bing Chat pirate-persona phishing · EchoLeak · Cursor RCE.

## Skills & mapping

`direct injection` · `indirect injection` · `format smuggling` · `zero-click AI exploits` · `agent tool abuse`

Primary role: **AI red-teamer / LLM penetration tester (prompt injection specialist)**. Secondary: **AI security researcher / risk communicator**.

## Reference

- OWASP LLM01 Prompt Injection: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- Simon Willison on prompt injection: https://simonwillison.net/series/prompt-injection/
- MITRE ATLAS AML.T0051: https://atlas.mitre.org/techniques/AML.T0051
