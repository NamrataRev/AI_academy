# Writing and Testing Specifications

## Writing and Testing Specifications

## Learning Objectives

By the end of this topic, you will be able to:

- Write clear AI specifications across different domains (health, transport, etc.).
- Test if the AI followed your instructions accurately.
- Iterate and improve your prompts when the AI's output is not quite right.

## Overview

Writing a prompt is easy, but writing a **specification** is a professional skill. A specification is a clear, structured set of instructions that leaves no room for AI guesswork. In this topic, we will look at how to write strong specifications across different industries, how to verify the AI's work, and what to do when the AI gets it wrong.

## 2.7 Writing Specifications Across Five Domains

**What Is It?**
A good specification (or "spec") always provides context, the exact task, and the desired format. 

**🚕 Think of it like this:** If you tell a taxi driver "take me to the city," you might end up anywhere. If you say "take me to 123 Main Street, avoid the highway, and drop me at the back entrance," you get exactly what you want. 

Here is how you write a tight specification in different fields:

- **Health:** "Act as a fitness coach. Write a 3-day beginner workout plan for someone with no equipment. Format the output as a table with columns for Day, Exercise, Sets, and Reps."
- **Transport:** "Draft a professional email to a logistics company asking for a quote to move 50 boxes from Mumbai to Delhi. Keep the tone polite but urgent, and keep it under 100 words."
- **Education:** "Summarise the water cycle for a 10-year-old. Use simple words and bullet points. Do not use complex scientific terms like 'precipitation' without explaining them first."
- **Food:** "Create a vegetarian dinner recipe using only paneer, tomatoes, and basic spices. List the exact measurements and provide step-by-step instructions. The total cooking time must be under 30 minutes."
- **Scheduling:** "Create a daily schedule for a student studying for exams. Block out 4 hours for studying, 1 hour for exercise, and 8 hours for sleep. Format it as an hourly timeline starting at 7:00 AM."

## 2.8 Testing a Specification: Did the AI Do What You Asked?

**What Is It?**
Testing means matching the AI's output against your original specification (remember the 15% 'Verify' step from the 70/30 rule).

**Rules for Testing:**
Never just read the output and say "looks good." Be a strict grader. 

1. **Check the constraints:** If you asked for under 100 words, did it obey?
2. **Check the format:** Did it give you a table, bullet points, or a timeline as requested?
3. **Check the tone:** Is it professional, or did it use slang when you told it not to?
4. **Check the facts:** Did it invent a detail you did not provide?

## 2.9 Iterating: Fixing Output Gaps

**What Is It?**
An "output gap" is the difference between what you *wanted* and what the AI *produced*. Iterating means adjusting your prompt to close that gap.

**Common Mistakes & How to Fix Them:**

- **Gap:** The AI's answer is too long and boring.
  - **Iteration:** Add a strict limit: *"Make it maximum 3 sentences. Use an energetic tone."*
- **Gap:** The AI gave generic advice instead of a specific plan.
  - **Iteration:** Add more context: *"You are an expert event planner. Give me a step-by-step checklist, not general advice."*
- **Gap:** The AI completely misunderstood the task.
  - **Iteration:** Break the task into smaller steps (Decomposition!): *"First, list the ingredients. Second, write the cooking steps."*

## Key Takeaway

- A **specification** is a precise set of instructions, unlike a casual prompt.
- **Testing** means strictly comparing the AI's output to your original rules (format, length, tone).
- **Iterating** is the process of adjusting your instructions to fix any mistakes or gaps in the AI's answer.
- The better your specification, the less time you spend iterating.

**Interview tip:** When discussing AI, do not say "I am good at prompting." Instead say, "I am good at writing strict specifications and iterating based on output gaps." This language immediately separates you from a beginner.
