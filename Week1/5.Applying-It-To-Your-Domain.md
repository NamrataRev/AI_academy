

# Applying It to Your Domain



## Learning Objectives

By the end of this topic, you should be able to:

- Pick a real-world domain you actually care about — healthcare, education, transport, banking, or anything else
- Apply decomposition, abstraction, and algorithmic thinking from the previous topics to a real problem in that domain
- Write a clear, focused 3-sentence problem statement
- Tell the difference between a strong, specific problem statement and a vague one
- Explain why getting the problem statement right early makes everything else in this program easier

---

## Overview

You've now covered the core building blocks of computational thinking — breaking problems apart, hiding unnecessary detail, expressing logic clearly, and understanding what makes a proper algorithm. This topic asks you to take all of that and apply it to something personal: **a domain you actually care about.**

Over the next 15 weeks, you'll build toward a Capstone project — a complete, working AI-powered system that you design and build yourself. That project has to start somewhere. It starts here, by choosing a domain and writing a precise **problem statement** before you touch a single line of code or an AI tool.

Why now, before you've even opened Python? Because a vague starting point always leads to a vague product. "I want to build something with AI in healthcare" sounds exciting but means nothing actionable. A sharp, well-scoped problem statement — written with the same discipline you just learned — sets you up to succeed at every later stage.

---

## Choosing Your Domain

A domain is simply an area or industry where a real problem exists — healthcare, banking, education, agriculture, transport, food delivery, or anything else.

You don't need to be an expert. You just need some familiarity or genuine curiosity. Here's how to pick one:

- Pick something you've personally experienced or observed — your own college life, a family member's business, a local community issue
- Prefer domains with real, observable problems — not abstract or theoretical ones
- Good starting areas for BTech freshers: student life and education, UPI and FinTech, healthcare, agriculture, railway booking, food delivery apps, or regional-language AI

The key point: AI-Native Engineers don't build "AI in general." They build AI-powered solutions for a specific problem, for specific users, in a specific context. Your domain gives your learning direction — every new concept from here (specifications, evaluation, agents) becomes easier when you can picture it in a context you actually care about.

---

## Writing a 3-Sentence Problem Statement

A problem statement is a short, precise description of a real problem — written clearly enough that anyone reading it understands exactly what the issue is, who faces it, and why it matters. Crucially, it does **not** describe how you'll solve it. That comes later.

Beginners almost always jump straight to the solution — "I'll build a chatbot!" — without ever clearly stating the problem that chatbot is supposed to solve. Writing the problem first, and forcing it into just three sentences, makes you decompose your idea down to its essential core before you get distracted by implementation.

**The 3-sentence structure:**

- **Sentence 1** — Who faces this problem, and what specifically goes wrong or is difficult for them today?
- **Sentence 2** — Why does this problem matter — what is the cost or consequence of leaving it unsolved?
- **Sentence 3** — What would "solving" this look like in plain terms, without yet mentioning the technology?

### Weak vs Strong — Side by Side

**Weak problem statement:**

> "Students have trouble with their studies. AI can help them learn better. We should build something for this."

This fails the Definite test from the Algorithmic Thinking topic. Which students? What specific difficulty? "Learn better" could mean a thousand different things.

**Strong problem statement:**

> "First-year engineering students in Tier-2 and Tier-3 Indian colleges often struggle to get quick answers to basic doubts outside class hours, since teaching assistants are not always available. This leads many students to either fall behind silently or rely on unverified answers from random online forums. A good solution would let a student ask a doubt in their own words, at any time, and receive an accurate, syllabus-aligned explanation they can actually understand."

Notice how this version applies everything from previous topics:

- **Decomposition** — it narrows "students" down to a specific group and a specific difficulty, not "education in general"
- **Definite language** — no vague words like "better" or "help" without explanation
- **Input / Output framing** — clear input (a student's doubt) and a clear desired output (an accurate, understandable explanation)

### Rules for a Good Problem Statement

- Name a **specific** group of people — not "everyone" or "students" in general
- Describe a **specific, observable** difficulty — not a general dissatisfaction
- Do **not** mention your intended solution or technology — no "using AI, we will build a chatbot that…"
- Keep it to exactly **three sentences** — this constraint forces clarity and prevents rambling

### Common Beginner Mistakes

- Writing a solution statement instead of a problem statement — jumping straight to "I will build an AI chatbot" without stating the actual problem
- Choosing a domain so broad ("healthcare") that a specific problem never gets identified
- Describing a problem no one actually experiences — always ground it in something real and observable

---

## Worked Example — Railway Travel

**Step 1 — Start broad (too vague):**

> "Train travel in India can be improved with AI."

Fails immediately — not decomposed, not definite.

**Step 2 — Decompose "train travel" into specific sub-areas:**

- ticket booking
- platform information
- delays and schedule updates
- luggage safety
- food quality

**Step 3 — Pick one specific, real sub-problem:**

Passengers on waitlisted tickets often don't know their real chances of confirmation and check repeatedly out of anxiety.

**Step 4 — Write the 3-sentence problem statement:**

> "Passengers with waitlisted railway tickets often have no clear sense of whether their ticket will be confirmed, so they repeatedly refresh the IRCTC app out of anxiety in the days before travel. This uncertainty causes unnecessary stress and makes it hard for passengers to plan backup travel options in time. A good solution would give waitlisted passengers a clear, realistic, and regularly updated sense of their confirmation chances well before the journey date."

**Step 5 — Verify against F.D.I.O. from the Algorithmic Thinking topic:**

- **Finite** — scoped to a specific window before the journey date, not open-ended
- **Definite** — names a specific group (waitlisted passengers) and a specific difficulty (no confirmation-chance visibility)
- **Input** — the passenger's ticket status and history are the implied input
- **Output** — a realistic, updated confirmation chance is the clear, expected output

This problem statement is now specific enough to carry forward into the next section, where you'll turn it into a full, testable AI specification.

---

## Key Takeaways

- Choose a domain you have some familiarity with or genuine curiosity about — healthcare, education, banking, agriculture, transport, and food delivery are all rich with real problems
- A good problem statement describes the **problem, not the solution** — never mention your intended technology in it
- Use exactly **3 sentences**: who + what's difficult, why it matters, what "solved" would look like
- Apply the discipline from this whole unit — decomposition to narrow the problem, definite language to avoid vagueness, F.D.I.O. as a sanity check
- A vague problem statement guarantees a vague and often useless AI solution later — precision here saves enormous effort down the line
- Ground your problem in something real — ideally something you've observed or experienced directly, not a guess
- This problem statement is the seed of your **Capstone project** — the more precise it is now, the smoother the rest of the course will be

> **Interview tip:** Being able to clearly articulate "the problem, not just the solution" is one of the most valued skills interviewers look for in junior AI and software engineering roles. Most freshers jump straight to "I'll build a chatbot" — knowing how to define the problem first makes you stand out.

## References
- [Asana: How to write a problem statement](https://asana.com/resources/problem-solving-strategies)
