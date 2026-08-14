# Planning Your Capstone Evaluation

---

## Learning Objectives

By the end of this topic, you should be able to:

- Explain why every AI system needs a written evaluation plan before it can be trusted or deployed
- Choose the right metric for a given AI system's purpose — accuracy, precision, recall, F1, or a human-rated rubric
- Design a complete evaluation plan including metric choice, test set size, and pass/fail threshold
- Explain the trade-offs involved in choosing a small vs large test set, and a strict vs lenient threshold

---

## Overview

Every concept you have covered in this unit — embeddings, similarity scores, precision, recall, F1, and calibration — exists to serve one final, practical purpose: helping you design a real evaluation plan for an AI system you build or oversee.

An evaluation plan answers three simple but critical questions, in writing, **before** your AI system reaches any real user:

1. **What will we measure?** — the metric
2. **How much evidence do we need before trusting the result?** — the test set size
3. **What result counts as good enough?** — the pass/fail threshold

Without answering these in advance, testing becomes vague and subjective. You end up judging quality by impression — "it seemed to work when I tried it a few times" — which is exactly the kind of unverified trust that leads to real AI failures.

**Think of it like a driving test.** A driving examiner does not watch you drive once and say "felt okay." They test a specific set of manoeuvres (the test set), score you on defined criteria (the metric), and have a fixed pass mark (the threshold) — all decided before you sit in the car. Your evaluation plan does the same thing for an AI system.

---

## What Is an Evaluation Plan?

An **evaluation plan** is a short written document — written before any testing begins — that specifies:

| Element | What it means |
|---|---|
| **Metric** | The specific number you will calculate to judge quality — accuracy, precision, recall, F1, or a human-rated rubric score |
| **Test set** | A fixed collection of example inputs with known correct outputs that you run the AI system against |
| **Test set size** | How many test cases are in your test set — more cases give more reliable results but take more time to prepare |
| **Pass/fail threshold** | The minimum score the system must achieve for you to consider it acceptable for its intended use |

---

## The Five-Step Framework

### Step 1 — Define what "correct" means for this system

This is the most important step — and the one most beginners skip.

For some tasks, "correct" has one exact right answer. For example, a system that classifies product images as "damaged" or "undamaged" either got it right or wrong — you can measure this precisely with accuracy, precision, and recall.

For other tasks, "correct" is more subjective. For example, a customer service reply chatbot — there is no single perfect answer. "Correct" means helpful, polite, and accurate — which requires a human to judge.

**Your decision here determines your entire metric choice:**
- One exact right answer → use a hard numeric metric (accuracy, precision, recall, F1)
- Subjective quality → use a human-rated rubric (e.g., rate each output 1 to 5, or simple pass/fail per output)

### Step 2 — Choose the metric that matches the cost of errors

You already know this from the previous topics — the right metric depends on which type of mistake is more costly:

- False negatives more dangerous → prioritise **recall**
- False positives more dangerous → prioritise **precision**
- Both matter roughly equally → use **F1** or overall pass rate
- Subjective output quality → use a **human-rated rubric**

**Example:** A job application screening AI that might unfairly reject strong candidates — false negatives (missing good candidates) are costly to applicants. You would prioritise recall and set a high recall threshold.

### Step 3 — Decide your test set size

Think of test set size like sample size in a survey. If you survey 3 people about their opinion on a film, you cannot trust that result. If you survey 300 people, you have a much more reliable picture.

For a course-level evaluation, use **at least 20–25 test cases** — enough to catch obvious failure patterns without requiring the effort of a full production-scale test suite. For a production AI system, companies typically use hundreds or thousands of cases.

**Always include edge cases alongside typical ones.** Edge cases are unusual, tricky, or boundary inputs — the situations most likely to expose a system's weaknesses. For example, for a language translation tool:
- Typical cases: straightforward sentences
- Edge cases: idioms that don't translate directly, very short one-word inputs, sentences with ambiguous meaning

If your test set contains only easy, typical examples and the system passes — you have not tested it properly.

### Step 4 — Set a pass/fail threshold and justify it in writing

Your threshold should reflect the real-world cost of failure for this specific system.

**Simple rule of thumb:**
- **High-stakes system** (health, finance, legal, academic integrity) → strict threshold, e.g., ≥ 90–95%
- **Medium-stakes system** (customer support, content recommendation) → moderate threshold, e.g., ≥ 80–85%
- **Low-stakes system** (casual feature, internal tool) → lenient threshold, e.g., ≥ 70–75%

Always write down **why** you chose this threshold — not just the number. "≥ 85% because this system makes customer-facing decisions but incorrect outputs can be quickly corrected by a human agent" is a real justification. "≥ 85% because it sounded good" is not.

### Step 5 — Write it all down before testing begins

This is not optional — it is the entire point.

If you decide your threshold **after** seeing your results, you will unconsciously lower the bar to make your system "pass." This is called goalpost-shifting and it is a well-documented bias in human judgment. The only way to avoid it is to commit to the threshold in writing before running a single test.

**The professional standard:** In enterprise AI deployments, the evaluation plan is reviewed and signed off by a team lead or stakeholder before any testing begins. The pass/fail threshold cannot be changed after testing starts without formal documentation of why.

---

## Two Worked Evaluation Plans

### Evaluation Plan 1 — Customer Support Chatbot (Medium Stakes)

**System purpose:** Answer common customer questions for an e-commerce platform — order tracking, return policy, delivery timelines.

| Element | Decision |
|---|---|
| **What does "correct" mean?** | Subjective — a human reviewer judges whether each answer is accurate and helpful |
| **Metric** | % of answers rated "accurate and helpful" by a human reviewer using a simple pass/fail rubric per question |
| **Test set size** | 25 questions: 10 about order tracking, 8 about returns and refunds, 5 about delivery, 2 edge cases (e.g., a question mixing two topics, or a question the system should correctly say "I don't have enough information — please contact support") |
| **Pass/fail threshold** | ≥ 80% — at least 20 out of 25 rated acceptable |
| **Why this threshold?** | Customer-facing but not safety-critical — an occasional imperfect answer is recoverable through follow-up. 80% ensures reliable usefulness while remaining achievable for a well-built system |

---

### Evaluation Plan 2 — Medical Triage Screening Tool (High Stakes)

**System purpose:** Flag patient intake forms that may indicate urgent medical attention needed — used by clinic reception staff to prioritise who sees a doctor first.

| Element | Decision |
|---|---|
| **What does "correct" mean?** | Objective — each form is either correctly flagged as urgent or not, verified against doctor review |
| **Metric** | Recall — missing a genuinely urgent case is far more dangerous than a false alarm that leads to an extra check |
| **Test set size** | 50 cases: 25 genuinely urgent cases, 25 non-urgent cases, including at least 5 edge cases (e.g., a patient with mild symptoms that mask a serious condition) |
| **Pass/fail threshold** | Recall ≥ 93% — the system must not miss more than 3–4 in every 50 genuinely urgent cases |
| **Why this threshold?** | Missing a genuinely urgent patient can cause serious harm. A false alarm means an extra doctor consultation — inconvenient but not dangerous. High recall threshold with human final decision required for every flag |

**Notice the difference between the two plans:**
- The chatbot uses a subjective human-rated rubric because there is no single right answer
- The triage tool uses recall because one type of mistake (missed urgent case) is far more dangerous than the other
- The triage threshold (93%) is stricter than the chatbot threshold (80%) because the stakes are higher

---

## Best Practices

- Always write the evaluation plan **before** building or testing the system — not after
- Include deliberately tricky edge cases in your test set — real failures usually hide there, not in the easy typical examples
- Match your threshold's strictness to the real-world cost of failure — higher stakes always demand a stricter threshold
- Re-run your evaluation plan whenever you make a meaningful change to the system's prompt or logic — a passing system today can silently fail after a change

## Common Beginner Mistakes

- **Testing with only 3–5 easy examples and declaring success** — too small a test set hides real failure patterns. This is like a driving examiner only watching you park once and saying you've passed
- **Choosing the pass/fail threshold after seeing results** — this is goalpost-shifting and undermines the entire point of evaluation
- **Using accuracy as the default metric for every system** — without checking whether precision, recall, or a human rubric better reflects what success actually means for that specific use case
- **Forgetting edge cases** — a system that handles typical inputs well but fails on unusual ones is not production-ready

---

## Key Takeaways

- An evaluation plan answers three questions in writing, before testing: **what metric**, **how much test data**, and **what score counts as passing**
- Match your metric to what "correct" means for that system — a hard numeric metric for objectively checkable outputs, a human rubric for subjective quality
- Use at least 20–25 test cases, always including deliberate edge cases
- Set your pass/fail threshold based on the real-world cost of failure — stricter for high-stakes systems, more lenient for low-stakes ones
- Always finalise the metric, test set, and threshold **before** testing begins to avoid unconscious goalpost-shifting
- The two worked plans above show how the same framework produces very different choices for different use cases — the framework is consistent, the decisions adapt to the context

> **Interview tip:** "How would you evaluate an AI system before deploying it?" is one of the most common entry-level AI engineering interview questions. Walk through the five steps: define correct, choose metric, decide test set size, set threshold, write it down before testing. Most candidates say "I would test it on some examples." You now have a structured, professional answer.

---

## Reference Links

- 📎 [Google Machine Learning Crash Course — Validation and Test Sets](https://developers.google.com/machine-learning/crash-course) — official grounding on why test data design matters
- 📎 [NIST AI Risk Management Framework — Measure Function](https://www.nist.gov/itl/ai-risk-management-framework) — official guidance on structured AI evaluation planning
- 📎 [Towards Data Science — How to Build a Machine Learning Evaluation Framework](https://towardsdatascience.com) — practical guidance on designing evaluation plans for real AI systems
