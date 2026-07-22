# Notes — Prompt Injection

## Task 2 — How LLMs Follow Instructions
- **Context window — five component types:** system prompts, developer prompts, user prompts, retrieved/RAG context, tool outputs.
- **Provider separation formats:** **ChatML** (role-based XML-like tags `<|im_start|>` / `<|im_end|>`, used by Qwen etc.); OpenAI's **Harmony** (explicit hierarchy: system > developer > user > assistant > tool).
- Core reality: separation is **convention-based formatting**, not a hard boundary — everything becomes one token stream.

## Task 3 — What is Prompt Injection?
- OWASP's **#1 LLM vulnerability**. Worked example: translation tool hijacked by "ignore the above instructions."
- Root cause: instruction-boundary conventions aren't enforced by architecture.
- **SQL-injection analogy:** it's an attack against the *application* the model is integrated with; risk scales with the app's granted capabilities (data/tool access).

## Task 4 — Prompt Injection in Action
- **Real incidents:** 2023 Bing "Sydney" system-prompt leak (Kevin Liu); 2022 remoteli.io Twitter bot hijack; Dec 2023 "$1 Chevrolet Tahoe."
- **Four direct techniques:**
  1. *Synonym/paraphrase overrides* — beat keyword blocklists (résumé-screening bypass).
  2. *Format-based injection* — hide instructions in HTML/markup/YAML (GitHub Copilot via hidden HTML tag in a GitHub issue).
  3. *Simulated dialogue injection* — forge a fake conversation history.
  4. *Multi-turn prompt shaping* — plant dormant instructions that activate later.
- Hands-on: replicate the $1-car attack against "LLMborghini."

## Task 5 — Indirect Prompt Injection
- Framed as "generative AI's greatest security flaw" — a system-level flaw in how apps ingest untrusted data.
- **Four ingestion vectors:**
  - *Web pages* — Bing Chat extension attack via invisible font-size-0 text (pirate-persona phishing).
  - *Emails/documents* — **EchoLeak** zero-click against Microsoft 365 Copilot.
  - *LLM agents/tools* — Cursor AI RCE via a shared Google Doc.
  - *RAG systems* — deeper in the Data Poisoning module.
- **Four consequences:** unauthorized actions, data leaks, content manipulation, zero-click exploits.

## Task 6 — Practical
- Exploit **CalBot** (internal calendar assistant) via indirect injection: a malicious calendar event description hides instructions that hijack CalBot's meeting summary to leak a restricted CEO email. See writeup.

## Task 7 — Conclusion
- Recap of context-window mechanics, prompt-injection definition, direct vs. indirect, and the real cases. Sets up **Jailbreaking** and later defense/mitigation.
