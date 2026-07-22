# Notes — Prompt Engineering

## Task 2 — LLM Fundamentals

- **Tokenization:** text → tokens (~3–4 chars) → token IDs. Schemes differ: GPT uses Byte-Pair Encoding, BERT uses WordPiece.
- **Nondeterminism:** same prompt can yield different outputs. Security implication: adversarial prompts *and* defenses must be tested repeatedly, not validated once.
- **Generation parameters:**
  - *Temperature* — randomness dial (low = deterministic, high = incoherent).
  - *Max tokens* — output length / cost ceiling.
  - *Top-p (nucleus sampling)* — alternative randomness control; don't combine with temperature.
  - *Context window* — the model's working-memory limit; overflow causes silent truncation.

## Task 3 — The Anatomy of a Prompt

- **Four pillars:** (1) instruction/task, (2) context, (3) output format, (4) constraints.
- Balance specificity vs. verbosity — vague prompts under-specify; bloated prompts waste context and confuse.

## Task 4 — System vs. User Prompts

- **System prompt** — persistent, sets role/behavior (developer-defined).
- **User prompt** — dynamic, task-specific.
- **Instruction hierarchy** is only a **probabilistic training convention** — the model sees one undifferentiated token stream, so "ignore your previous instructions" can break the hierarchy.
- Example: a security log analyzer hijacked by injected instructions inside log data. This is the seed of prompt injection (OWASP LLM01).

## Task 5 — Advanced Prompting Techniques

- **Shot spectrum:** zero-shot, one-shot, few-shot (in-context learning). Security examples: log severity classification, vulnerability JSON extraction, auth event classification.
- **Chain-of-Thought (CoT):** "Let's think step by step" (Google, 2022). Effective above ~100B parameters; underlies reasoning models (OpenAI o1, Anthropic extended thinking). Great for structured incident/log triage.
- **Prompt templates:** standardize recurring tasks (e.g., a reusable code-security-review template).

## Task 7 — Conclusion

- Recap of tokens, nondeterminism, four pillars, instruction hierarchy limits, and parameters.
- Bridges to **AI Forensics** and its DFIR challenge ("contAInment").
