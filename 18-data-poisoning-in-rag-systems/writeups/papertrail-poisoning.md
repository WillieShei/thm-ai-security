# Walkthrough — PaperTrail Knowledge-Base Poisoning (Task 7)

> Agent lab: poison a RAG assistant's knowledge base so it repeats a weakened security policy.
>
> **Note:** flags/answers redacted per THM policy. Documents method.

## Objective

Demonstrate data (knowledge-base) poisoning: without touching model weights or the system prompt, make the assistant give a weakened answer by corrupting what it retrieves.

## Method

1. **Baseline.** Ask the assistant a normal question (e.g., the password-reset policy) and record the correct answer.
2. **Inject a poisoned document.** Add a fake "policy revision" to the knowledge base that weakens the controls — e.g., longer rotation window, shorter minimum length, no special characters required, an external reset portal, email-only auth.
3. **Re-query.** Ask the same question again. Because retrieval ranks the poisoned "revision" highly, the assistant now repeats the **weakened** policy as authoritative.
4. **Confirm the mechanism.** Nothing about the model changed — only the retrieved reference material. The component modified is the **knowledge base / reference material**; the attack class is **data (knowledge-base) poisoning**.

## Techniques / concepts applied
RAG knowledge-base poisoning · retrieval abuse · demonstrating that the model trusts retrieved content by placement · behavioural change without weight/prompt modification.
