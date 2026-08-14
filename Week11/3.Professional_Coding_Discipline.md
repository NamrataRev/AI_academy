# Professional Coding Discipline

---

## Learning Objectives

By the end of this topic, you should be able to:

- Explain why writing a plain-English specification before writing or AI-generating code is a professional discipline, not an optional extra step
- Describe the golden rule of AI-native coding and why it protects you professionally
- Identify edge cases for a simple program and predict how the program should behave at each one
- Evaluate a piece of AI-generated code against a specification and decide whether it is safe to run
- Apply spec-first discipline and edge-case testing to a small Python program

---

## Overview

You now know enough Python — variables, data types, `if/else`, and `for` loops — to write small working programs. But knowing the syntax of a language is not the same as coding professionally.

This matters more, not less, now that AI can write code for you. In an AI-native workflow, you will frequently ask Claude to generate a Python function. That is completely normal and expected — **AI implements, you specify and verify.** But "verify" is not a suggestion — it is your core professional responsibility. If you cannot explain what a piece of code does, you have no way to catch a mistake in it. Mistakes in AI-generated code can cause real damage: a wrong account balance, a wrongly rejected application, exposed private data.

This topic teaches you three linked habits:
- Writing your specification **before** code exists
- Refusing to run code you cannot explain — the golden rule
- Deliberately testing the edges of what your program is supposed to handle

These three habits will follow you through every remaining week of this program and every real AI-native engineering job afterward.

**How the three habits work together:**

The three habits are not independent — they form a single workflow. You write the specification first so you know what correct looks like. You apply the golden rule so you actually read and understand the code before trusting it. You test edge cases so you verify the code against the full range of inputs the spec covers — not just the easy ones. Skip any one of the three and the other two become weaker. All three together is what professional, trustworthy AI-assisted coding looks like.

---

## Real World Application

**An e-commerce platform deploys an AI-generated discount function**

A developer asks an AI to generate a function that applies a 20% discount to orders above $100. The AI produces the function in seconds. Without spec-first discipline, the developer never wrote down what "above $100" means — does $100 exactly get the discount or not? Without the golden rule, the function goes straight into production without being read line by line. Without edge-case testing, nobody checks what happens for a $0 order, a negative amount (a return), or a non-numeric input.

Three weeks later, customers discover that orders of exactly $100 are not getting the discount — because the AI used `>` instead of `>=`. And a data entry error that sent `-50` as an order value caused the function to apply a "discount" that added money to the total instead of subtracting it.

All three failures were preventable:
- Spec-first would have forced the developer to write "discount applies at $100 and above" — making `>=` unambiguous
- The golden rule would have caught `>` vs `>=` during the line-by-line read
- Edge-case testing would have caught the negative amount issue before any real customer was affected

This is the exact workflow — spec → golden rule → edge cases — that prevents real production bugs from reaching real customers.

---

## Spec-First Discipline

**Spec-first discipline** means writing a clear, plain-English specification of what a piece of code should do — its inputs, its expected output, and its failure conditions — *before* you write a single line of code, and before you ask an AI to write it for you.

**A real-life analogy:**
Think about ordering food at a restaurant. You tell the waiter exactly what you want — "a chicken burger, no onions, with fries, medium spicy" — before they go to the kitchen. You do not say "make me something nice" and hope the chef guesses correctly. Spec-first discipline is the same idea applied to code. The more precisely you describe what you want, the more likely you are to get it.

**Why this discipline exists:**
Without a specification, both you and an AI model are guessing at what "done" looks like. Look at the difference between a wish and a specification:

| Bad — a wish | Good — a specification |
|---|---|
| "Write code to check a transaction" | "Write a Python function `check_transaction(amount)` that returns the string `'Needs Verification'` if `amount` is greater than 5000, otherwise returns `'Approved'`. Input is always a positive number." |
| "Make a loop for scores" | "Write a Python `for` loop that computes the average of a list of integer scores and prints `'Pass'` if the average is 40 or above, otherwise `'Fail'`." |

Notice the good versions state: the exact function name, the exact inputs, the exact expected outputs, and any assumptions about what values are allowed. This is what allows you to verify the resulting code afterward — you know precisely what correct was supposed to look like.

**How to write a spec for code — three things you must always include:**
1. **Inputs** — what does the function receive? What type? What range is valid?
2. **Expected output** — what exactly should it return or print for a given input?
3. **Failure conditions** — what should happen for invalid input? What is outside the contract?

---

## The Golden Rule — Never Run Code You Cannot Explain Line by Line

**The rule stated plainly:** Never run a piece of code — whether you wrote it, copied it, or an AI generated it — unless you can explain out loud what every single line does.

**Why this exists:**
Code executes with real consequences. It can delete a file, send real money, expose private data, or make a decision about a real person. An AI model like Claude is very good at producing code that looks correct and often is correct — but it can also make mistakes or misunderstand your intent. Your job as the human in the loop is to catch what the AI could have gotten wrong. You can only do that if you actually understand the code in front of you.

**A short worked example — code you should question before running:**

Imagine you asked an AI: *"Write a Python function that removes a student's record from our results file if their score is below 40."*

The AI gives you back:

```python
import os

def remove_failed_record(filename):
    os.remove(filename)
```

**Stop. Do not run this yet.** Walk through it line by line:

- `import os` — brings in Python's built-in `os` module, which lets your code interact with the operating system — files, folders, and more
- `def remove_failed_record(filename):` — defines a function named `remove_failed_record` that takes one input, `filename`. (`def` is the Python keyword for "define a function" — it tells Python: "the indented lines below are a reusable block of instructions with this name")
- `os.remove(filename)` — this line **permanently deletes the entire file** named by `filename` from storage

Compare this to your specification: you asked to remove one student's record from within a file — not delete the entire file. This code is dangerously wrong. Running it would destroy the whole results file for every student, not just the one who failed.

This is exactly why the golden rule exists. If you had simply run this code because "the AI wrote it, so it must be right," you could have caused serious, irreversible damage.

### Best Practices

- Read every line of AI-generated code before running it — treat it exactly as you would treat code from a stranger on the internet
- If any single line's purpose is unclear, look it up or ask the AI to explain that specific line **before** running it — never after
- Be especially cautious of any code that deletes, overwrites, or sends data — these operations are the most serious and often irreversible
- Run new or AI-generated code on sample data first — never directly on real data

### Common Beginner Mistakes

- Copy-pasting code from an AI chat window straight into a program handling real data, without reading it
- Assuming that because code runs without an error, it must be doing the correct thing — a program can run perfectly and still produce the wrong result if the logic does not match the specification
- Trusting AI output more because it sounds confident — AI text generation is probabilistic and can be fluently, confidently wrong

---

## Edge Cases — Testing the Boundary of Expected Input

**An edge case** is an input at the extreme boundary of what a program is supposed to handle — not the everyday typical input, but the unusual, extreme, or unexpected ones.

**A real-life analogy:**
Think about a lift (elevator). The everyday use is one or two people pressing a floor button. Edge cases are what happens when 15 people get in at once, when someone presses every floor, when the power cuts out mid-journey, or when someone tries to go to a floor that does not exist. A lift that only works under normal conditions is not a safe lift. A program that only works for typical inputs is not a trustworthy program.

**Why edge cases matter:**
The "happy path" — testing with a typical, expected input — almost always works. That is the easy part. Real bugs live at the edges. A discount function that works for $50 might silently produce a negative discount for $0, or crash entirely if someone accidentally passes in a text string instead of a number.

**Standard edge cases to always test:**

| Edge case | Why it matters |
|---|---|
| **Zero** | Many calculations break or behave unexpectedly at zero |
| **Negative number** | Often invalid — does the code handle it gracefully or silently compute nonsense? |
| **Maximum realistic value** | Does the code still work at the upper boundary? |
| **The exact boundary value** | If the spec says "40 or above," test exactly 40 — not just 39 and 41 |
| **Empty list** | A loop over an empty list should not crash |
| **Wrong data type** | What happens if a number was expected but a string was passed? |

### Worked Edge Case Analysis — Shipping Cost Calculator

**Specification:** "Write a Python function `calculate_shipping(weight_kg)` that takes a package weight in kilograms (a positive number) and returns the shipping cost in dollars: $5 if the weight is 1kg or below, $10 if between 1kg and 5kg (exclusive), and $20 for 5kg and above."

**The function:**

```python
def calculate_shipping(weight_kg):
    if weight_kg <= 1:
        return 5
    elif weight_kg < 5:
        return 10
    else:
        return 20
```

**Edge case testing:**

| Input | Expected | Actual | Verdict |
|---|---|---|---|
| `2` — typical case | `10` | `10` | ✅ Correct |
| `1` — exact lower boundary | `5` | `5` | ✅ Correct — confirms `<=` is right, not `<` |
| `5` — exact upper boundary | `20` | `20` | ✅ Correct — confirms `>=` in the else |
| `0` — zero weight | `5` (returns standard rate) | `5` | ✅ Runs — but is a 0kg package realistic? Flag as a specification gap |
| `-2` — negative weight | Undefined by spec | `5` | ⚠️ Runs silently — produces a nonsensical result. The spec never said what to do with negative input |
| `"heavy"` — wrong type | Undefined by spec | `TypeError` | ⚠️ Crashes — a string cannot be compared to a number |

**What the edge cases revealed:**
The function is correct for all valid inputs. But testing found two real gaps:
- Negative weights run silently and return a meaningless result
- String input crashes the program

These are not code bugs — they are **specification gaps**. The spec never stated what should happen for invalid input. A professional engineer goes back and updates the specification first, then fixes the code:

```python
def calculate_shipping(weight_kg):
    if not isinstance(weight_kg, (int, float)):
        return "Error: weight must be a number"
    if weight_kg <= 0:
        return "Error: weight must be a positive number"
    if weight_kg <= 1:
        return 5
    elif weight_kg < 5:
        return 10
    else:
        return 20
```

**What `isinstance()` does:**
`isinstance(weight_kg, (int, float))` checks whether `weight_kg` is either an integer or a float — in other words, whether it is actually a number. If someone passes in `"heavy"` (a string), `isinstance` returns `False`, so the `not isinstance(...)` condition becomes `True` and the function returns an error message immediately, before trying to do any comparison. This is called **input validation** — checking that the input is the right type before using it.

---

## Worked Example — Attendance Eligibility Checker

**Specification:** "Write a Python function `classify_attendance(percentage)` that takes a student's attendance percentage (a number from 0 to 100) and returns `'Eligible'` if it is 75 or above, otherwise returns `'Not Eligible'`."

**Step 1 — Explain `def` and `return` before reading the code:**

`def` is the Python keyword for defining a function — a reusable block of code you can call by name. Every function definition follows the same pattern:

```python
def function_name(input):
    # code that runs when you call this function
    return result
```

You call the function by writing its name with an input in brackets: `classify_attendance(80)`

**`return` vs `print()` — a very common beginner confusion:**

These two look similar but do completely different things:

- `print()` — displays something on screen for you to see. The value disappears after being shown — it cannot be used anywhere else in the program
- `return` — sends a value back to whatever called the function, so it can be stored, compared, or used in the next step

Think of it like this. `print()` is like reading a number out loud — someone hears it, but it is gone. `return` is like writing the number on a piece of paper and handing it back — the caller can now use it.

```python
# Using return — the result can be stored and used
result = classify_attendance(80)
if result == "Eligible":
    print("Student can sit the exam")

# Using print inside the function — the result disappears after display
# and cannot be checked or stored
```

In real programs, almost every function uses `return` — not `print()` — so the result can be used in the next step of the code.

**Step 2 — The code matching the spec:**

```python
def classify_attendance(percentage):
    if percentage >= 75:
        return "Eligible"
    else:
        return "Not Eligible"

print(classify_attendance(80))    # test 1
print(classify_attendance(75))    # test 2 — exact boundary
print(classify_attendance(60))    # test 3
```

**Expected output:**
```
Eligible
Eligible
Not Eligible
```

**Step 3 — Golden rule check — explain every line:**

- `def classify_attendance(percentage):` — defines a function that accepts one input, `percentage`
- `if percentage >= 75:` — checks whether the input meets the threshold. `>=` includes exactly 75, matching "75 or above"
- `return "Eligible"` / `return "Not Eligible"` — sends back one of two possible strings, exactly as the spec requires
- The three `print()` calls test three different inputs — including the exact boundary value 75

**Step 4 — Edge case testing:**

| Input | Expected | Actual | Verdict |
|---|---|---|---|
| `100` — maximum | `'Eligible'` | `'Eligible'` | ✅ |
| `75` — exact boundary | `'Eligible'` | `'Eligible'` | ✅ Confirms `>=` not `>` |
| `74.9` — just below | `'Not Eligible'` | `'Not Eligible'` | ✅ |
| `0` — minimum | `'Not Eligible'` | `'Not Eligible'` | ✅ |
| `-5` — invalid | Undefined by spec | `'Not Eligible'` | ⚠️ Specification gap |
| `105` — impossible | Undefined by spec | `'Eligible'` | ⚠️ Specification gap |

**Conclusion:** The function is correct for all valid inputs. Edge-case testing revealed the same type of gap as the shipping example — the spec never stated what should happen for values outside 0–100. Before using this on real student data, the specification should be updated to handle invalid input explicitly.

---

## Key Takeaways

- **Spec-first discipline** means writing clear inputs, expected outputs, and failure conditions **before** writing or AI-generating any code
- A specification is not a wish — it must state the exact function name, input type, expected output, and what happens for invalid input
- The **golden rule** — never run code you cannot explain line by line. AI-generated code can be confidently wrong, and code executes with real consequences
- `def` defines a reusable function in Python. You call it by name with inputs in brackets
- `return` sends a value back to the caller so it can be stored and used. `print()` only displays — the value disappears after being shown. Real functions almost always use `return`
- `isinstance(value, type)` checks whether a value is of a specific type — used for input validation before doing any calculations
- An **edge case** is an input at the extreme boundary — zero, negative, maximum, exact boundary value, empty list, wrong type
- Testing only the happy path gives false confidence — most real bugs live at the edges
- Always test the **exact boundary value** stated in the specification — using `>` instead of `>=` is one of the most common real bugs
- When an edge case reveals undefined behaviour, treat it as a **specification gap** — fix the spec first, then fix the code
- The three habits work together as one workflow: spec-first → golden rule → edge-case testing. Skip any one and the others become weaker

> **Interview tip:** Interviewers frequently ask "what edge cases would you test for this function?" Have a ready checklist: zero, negative, maximum, exact boundary, empty list, wrong type. This checklist will serve you in almost every technical interview.

---

## Reference Links

- 📎 [Python Official Documentation — Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions) — official reference on function syntax
- 📎 [W3Schools — Python Functions](https://www.w3schools.com/python/python_functions.asp) — beginner-friendly supplementary reading on function syntax
- 📎 [Real Python — How to Write Pythonic Code](https://realpython.com/python-pep8/) — professional Python coding standards and habits
- 📎 [Anthropic Documentation — Claude API](https://docs.anthropic.com/) — for reference when you begin reviewing AI-generated code using Claude's API
