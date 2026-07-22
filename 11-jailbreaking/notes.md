# Notes — Jailbreaking

## Task 2 — Prompt Injection vs Jailbreaking
- **Willison's distinction:** prompt injection = concatenation of trusted + untrusted strings (attacks the app integration); jailbreaking = targets the model's own safety filters directly, no concatenation needed.
- Precise classification = accurate vuln reporting (echoes the OWASP misclassification exercise in Room 6).

## Task 3 — Why Models Have "Jails"
- **Safety alignment via RLHF** is probabilistic pattern-learning, **not** enforced rules.
- **Fragility:** activation-space "ablation" removes specific safety directions; fine-tuning on **1,000 benign samples** can degrade safety by **60%+** (ties to Room 3's inheritance problem).
- **Helpfulness–harmlessness paradox / "alignment tax."**
- **Safe RLHF** — dual reward models as an attempted fix.
- Willison: "you cannot use a language model to perfectly filter the output of the same language model."

## Task 4 — Classic Jailbreak Techniques (with cited success rates)
1. **Roleplay/persona** — 87.3% open-source, 84.3% commercial; fiction-writer & authority-figure personas strongest.
2. **"Grandma exploit"** — emotional manipulation + fictional/historical framing; research on 40 persuasion techniques shows 92% for emotional appeals; counterintuitively, GPT-4 and more advanced models are *more* susceptible to persuasion.
3. **Obfuscation/encoding** — Base64, leetspeak/char substitution, low-resource languages (Zulu, Swahili, Gaelic — safety training is English-centric), word fragmentation across token boundaries.
4. **Instruction sandwiching** — bury the harmful request among benign multi-part tasks.
- Hands-on: submit three of these techniques for assessment.

## Task 5 — Multi-turn Jailbreaking & Conditioning
- **Consistency bias:** multi-turn beats single-turn by 10–20%.
- **Five strategies:** trust-building (foot-in-the-door), gradual escalation (**Crescendo**, 89%), context shaping ("poisonous seeds"), trigger phrases (exploit the model's own prior outputs), backtracking/adaptation on refusal.

## Task 6 — Case Study: DAN
- "Do Anything Now" — Reddit origin Dec 2022 (u/seabout); "token system" gamification in **DAN 5.0** (Jan 2023); cited in Wei et al. 2023; crackdown as r/chatGPTJailbreaks banned Dec 2025.
- Shows grassroots adversarial research outpacing/informing formal industry practice.

## Task 7 — Challenge (TryJailbreakMe)
- Capstone: combine techniques to make a chatbot reveal a secret flag it was told not to disclose. See writeup.

## Task 8 — Conclusion
- Recap: alignment as statistical tendency, classic techniques, multi-turn conditioning, DAN. Sets up the module's defensive **Prompt Defence** room.
