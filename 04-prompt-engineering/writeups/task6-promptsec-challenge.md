# Walkthrough — PromptSec Challenge (Task 6)

> Graded practical: apply an assigned prompting technique to a security task, scored /10 per attempt. Accumulate 40 points to earn the flag.
>
> **Note:** flag redacted per THM policy. Documents approach.

## Objective

Across multiple mini-challenges, the PromptSec chatbot assigns you a specific technique (e.g., few-shot, Chain-of-Thought) and a security task (e.g., classify log severity, extract vulnerability data as JSON). Write a prompt that correctly applies the technique; earn points; reach 40 total → flag.

## Approach

1. **Read the assigned technique carefully.** Points are for *correct technique application*, not just a correct-looking answer. If told "few-shot," you must include labeled examples.
2. **Apply the four pillars every time.** State the instruction, give context, define output format, set constraints — even under a specific technique.
3. **Technique cheat-sheet used:**
   - *Zero-shot* — clear instruction, no examples.
   - *Few-shot* — 2–3 labeled input→output examples before the real input.
   - *Chain-of-Thought* — request explicit step-by-step reasoning ("think step by step") for triage/classification tasks.
   - *Output format* — for extraction tasks, pin a strict schema (e.g., JSON with named fields).
4. **Iterate on feedback.** The score/feedback loop mirrors real prompt evaluation (promptfoo-style rubrics). Adjust phrasing to lift the score toward 10.
5. **Accumulate 40 points** across challenges → flag `THM{<redacted>}`.

## Techniques / concepts applied

- Four-pillar prompt construction under constraint
- Few-shot in-context learning; Chain-of-Thought
- Rubric-driven prompt iteration/evaluation

## Result

40+ points reached; flag captured. This is the closest the path comes to a graded "prompt engineer" competency check.
