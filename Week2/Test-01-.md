# What Makes a Good Specification

*Specifying for AI — BTech Semester 1*

---

## Learning Objectives

By the end of this topic, you should be able to:

1. Explain what a specification is and why it is the most important skill for anyone who directs AI to do work
2. Identify the four properties of a good specification — Testable, Bounded, Observable, Actionable (T.B.O.A.)
3. Tell the difference between a vague, weak specification and a precise, professional one
4. Break any task down into its inputs, expected outputs, and failure conditions before asking AI to do it
5. Write a well-formed specification for a simple real-world task
6. Look at an existing specification and spot what is missing from it

---

## Overview

You already know that AI systems are probabilistic — they generate the most *likely* answer, not a guaranteed one. That single fact leads to the most important skill in this entire program: **if you don't tell an AI system precisely what you want, it will guess — and its guess may not match what you actually needed.**

Think about ordering food on Swiggy. If you just type "send me food," the app has no idea what to do. But the moment you say "1 Paneer Butter Masala, 2 Butter Naan, deliver to Hostel Block C, Room 204, by 8 PM" — it knows exactly what to do. That second instruction is a specification.

A **specification** (often called a "spec") is a clear, precise description of what you want a system to do, written *before* you ask the AI to build or do anything. The AI cannot write a good spec for you — only you know what "good" actually means for your problem. Every time an AI does the wrong thing, it almost always traces back to a spec that was incomplete, vague, or untestable.

---

## What Is a Specification?

A specification is a written description of a task that states exactly:
- what input the system will receive
- what output it must produce
- what should happen when something goes wrong

It must be precise enough that two different people — or two different AI systems — reading it would build the *same* thing.

Human language is naturally vague. If you tell a friend "get me something to eat," they might bring you biryani, a sandwich, or biscuits — all technically valid. That looseness is fine between friends, but it fails badly when you're directing a powerful, literal system that acts on your exact words. A specification removes the vagueness *before* the work begins, not after you're disappointed with the result.

---

## The Four Properties of a Good Specification (T.B.O.A.)

A specification is only useful if it has all four of these properties. Miss even one and you open the door to a result you didn't want. Memorise them as **T.B.O.A.**

- **Testable** — you can check, with a clear yes or no, whether the output meets the requirement. Ask yourself: "Can I write a test that proves this was done correctly?"
- **Bounded** — the task has clear limits — a maximum length, a specific scope, a defined set of inputs it must handle. Ask yourself: "Does this say how big, how long, or how much?"
- **Observable** — you can actually see or measure the output to judge it. Ask yourself: "Can I look at the result and judge it against the spec?"
- **Actionable** — the instruction tells the system what to *do*, not just what outcome you vaguely wish for. Ask yourself: "Does this tell the system a concrete action to take?"

**Real-life analogy:** Imagine giving directions to a Swiggy delivery partner. "Go somewhere near Koramangala" is not testable, bounded, observable, or actionable — the rider has no idea if they've succeeded. "Deliver to Flat 302, Sunrise Apartments, 80 Feet Road, Koramangala 4th Block, by 8:00 PM" gives them everything they need. That is a specification.

<div style="display:flex;align-items:flex-start;gap:24px;margin:16px 0">
<div style="flex:1">

```mermaid
flowchart TD
    A[Specification] --> B[Testable\nCan I verify it?]
    A --> C[Bounded\nAre there clear limits?]
    A --> D[Observable\nCan I see the output?]
    A --> E[Actionable\nDoes it say what to DO?]
```

</div>
<div style="flex:1">

**Remember it as T.B.O.A.**

Think of it like a Zomato order:
- **Testable** — did the right dish arrive?
- **Bounded** — is it within the delivery area and time?
- **Observable** — you can see and taste it
- **Actionable** — "deliver Paneer Masala to Room 204" is a concrete action

</div>
</div>

---

## Bad Spec vs Good Spec

This is the most common beginner mistake — writing a wish instead of a specification.

**Bad specification:** *"Make it better."*

This fails all four properties:
- Not testable — "better" according to what measure?
- Not bounded — better by how much, in what way?
- Not observable — there's no way to check against a fixed standard
- Not actionable — it tells the AI nothing about what action to take

**Good specification:** *"Rewrite this paragraph at a Grade 8 reading level, using simple sentences, keeping the meaning unchanged, in no more than 80 words."*

This passes all four:
- Testable — you can run a readability check and count the words
- Bounded — hard limit of 80 words is given
- Observable — you can read the result and compare it against "Grade 8 level" and word count
- Actionable — "rewrite," "use simple sentences," and "keep the meaning unchanged" are concrete actions

**More real-world examples you'll actually relate to:**

<div style="display:flex;align-items:flex-start;gap:24px;margin:16px 0">
<div style="flex:1">

**Bad specs ❌**
- "Make the order confirmation message nicer."
- "Warn students who are missing too much class."
- "Handle failed UPI payments well."

</div>
<div style="flex:1">

**Good specs ✅**
- "Rewrite the order confirmation SMS to be under 160 characters, include the order ID and expected delivery time, and use a friendly but professional tone."
- "Send an email alert to any student whose attendance falls below 75% in any subject, listing the subject name and current percentage, sent every Friday at 6 PM."
- "If a UPI payment fails, show the user the specific reason — insufficient balance, bank server down, or incorrect PIN — within 3 seconds, and offer a Retry button."

</div>
</div>

---

## Inputs, Expected Outputs, and Failure Conditions

Every good specification, no matter the domain, breaks into three parts. Ask these three questions before specifying any task:

```mermaid
flowchart LR
    A[What INPUT\nwill it receive?] --> B[What OUTPUT\nmust it produce?]
    B --> C[What FAILURE CONDITIONS\nmust it handle?]
    C --> D[Complete, testable\nspecification]
```

- **Input** — what information does the system start with? For example: a student's marks, a scanned ID card, a customer's order details
- **Expected output** — what exact result must come out the other end? For example: a confirmation SMS, an approval or rejection decision, a formatted report
- **Failure conditions** — what could go wrong, and what should happen in each case? A specification that only describes the "happy path" — when everything goes right — is an incomplete specification. Real systems fail in real ways, and your spec must say what correct failure behaviour looks like too

**Worked breakdown — IRCTC ticket refund:**

- Input: ticket PNR number, cancellation date, ticket fare, class of travel
- Expected output: refund amount calculated per Indian Railways cancellation rules, displayed to the user within 5 seconds
- Failure conditions: invalid PNR → show "PNR not found" error; cancellation after chart preparation → show "no refund eligible, contact TDR"; system timeout → show "please retry" with no silent failure

### Rules for a Good Specification

- Always write the specification down in text — do not keep it in your head. A written spec can be reviewed, tested, and reused
- Write the failure conditions *before* you ask the AI to build anything — most real-world bugs come from unhandled failure cases, not the happy path
- Keep specifications as short as possible while still being complete — a bloated spec is as hard to verify as a vague one

### Common Beginner Mistakes

- Writing goals instead of specifications — "improve user experience" instead of a concrete, testable instruction
- Forgetting to define what "done" looks like — without an observable success criterion, you cannot verify the AI's output
- Specifying only the happy path and being surprised when edge cases produce bad results

> A specification is not the same as a wish. A wish describes a feeling — "users should feel the app is trustworthy." A specification describes an action and a measurable outcome — "display the total amount debited in bold, immediately after every UPI transaction." Your job is to translate wishes into specifications.

---

## Real World Applications

<div style="display:flex;align-items:flex-start;gap:24px;margin-bottom:24px">
<div style="flex:1">

**Banking / UPI**
Specifying exactly how a UPI failure message should be worded, when it should appear, and what information it must contain. Ambiguity here causes real customer confusion and complaints.

</div>
<div style="flex:1">

```mermaid
flowchart TD
    A[UPI Payment fails] --> B{Reason?}
    B -- Insufficient balance --> C[Show specific error\nwithin 3 seconds]
    B -- Bank server down --> C
    B -- Incorrect PIN --> C
    C --> D[Show Retry button]
```

</div>
</div>

<div style="display:flex;align-items:flex-start;gap:24px;margin-bottom:24px">
<div style="flex:1">

**College attendance system**
Specifying an alert tool — bounded to 75% threshold, testable against attendance records, observable in the email sent, and actionable with a concrete trigger every Friday at 6 PM.

</div>
<div style="flex:1">

```mermaid
flowchart TD
    A[Every Friday 6 PM] --> B[Check attendance\nfor all students]
    B --> C{Below 75%\nin any subject?}
    C -- Yes --> D[Send email alert\nwith subject and %]
    C -- No --> E[No action]
```

</div>
</div>

<div style="display:flex;align-items:flex-start;gap:24px">
<div style="flex:1">

**E-commerce returns**
Specifying that a return-eligibility checker must classify an order as "eligible," "not eligible," or "needs manual review" — covering every possible order status as a failure condition.

</div>
<div style="flex:1">

```mermaid
flowchart TD
    A[Return request raised] --> B{Item status?}
    B -- Damaged --> C[Eligible]
    B -- Within return window --> D[Eligible]
    B -- Outside return window --> E[Not eligible]
    B -- Unclear --> F[Needs manual review]
```

</div>
</div>

---

## Worked Example — Weekly Assignment Reminder

**Scenario:** Write a specification for an AI tool that sends a weekly summary email to college students listing their pending assignments.

**Step 1 — Identify the input:**
A list of assignments with subject name, due date, and submission status — submitted or pending.

**Step 2 — Identify the expected output:**
A plain-text email, no more than 120 words, listing only pending assignments sorted by due date (soonest first), with the subject line "Your Pending Assignments This Week."

**Step 3 — Identify the failure conditions:**
- If there are zero pending assignments → send a short congratulatory message instead of an empty list
- If a due date is missing or invalid → exclude that assignment and add a note: "1 assignment could not be checked — please verify manually"
- If the assignment list fails to load → do not send any email, and instead alert the system administrator

**The final specification:**

> "Generate a plain-text weekly email, subject line 'Your Pending Assignments This Week,' listing only assignments marked 'pending,' sorted by due date (soonest first), maximum 120 words. If zero assignments are pending, send: 'Great job — you have no pending assignments this week!' If any assignment has a missing or invalid due date, exclude it and append: '[N] assignment(s) could not be checked — please verify manually.' If the assignment data fails to load entirely, do not send the email and log an alert for the system administrator instead."

Notice how this single paragraph is testable (check word count and sorting), bounded (120-word limit, specific subject line), observable (read the email and compare line by line), and actionable (every instruction tells the system exactly what to do).

---

## Key Takeaways

- A specification is a precise, written description of a task — input, output, and failure conditions — given to an AI system before it starts working
- A good specification is **Testable, Bounded, Observable, and Actionable** — remember it as **T.B.O.A.**
- "Make it better" is a wish, not a specification. "Rewrite at Grade 8 level, max 80 words" is a specification
- Every task specification must cover three parts: **input → expected output → failure conditions**
- Specifying only the happy path and ignoring failure conditions is one of the most common and costly beginner mistakes
- Writing specifications is a 100% human responsibility — the AI cannot write its own requirements
- This skill directly connects to everything you build later in this program — a vague spec guarantees a useless AI output

> **Interview tip:** If asked "how do you ensure AI produces reliable output?", the strongest answer starts with "by writing a precise, testable specification before any AI call is made" — not with a technical fix after the fact.
