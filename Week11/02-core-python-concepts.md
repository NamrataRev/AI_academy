# Core Python Concepts

---

## Learning Objectives

By the end of this topic, you should be able to:

- Explain what a variable is and why programs need a way to store values
- Differentiate between the four basic Python data types — string, integer, float, and boolean
- Implement decision logic in Python using `if`, `elif`, and `else` statements
- Implement a `for` loop to repeat an action across every item in a list
- Use `range()` to repeat an action a fixed number of times
- Debug simple beginner mistakes involving indentation, data types, and comparison operators
- Create a short Python program that combines variables, data types, conditions, and a loop

---

## Overview

In the previous topic, you ran your very first line of Python code in Google Colab. Now we build the four foundational building blocks that every Python program — no matter how advanced — is made of:

- **Variables** — storing information
- **Data types** — the different kinds of information you can store
- **If/else** — making decisions
- **For loops** — repeating actions

These are not just beginner topics you outgrow. They are the vocabulary you will use every day as an AI-native engineer. When you write code around an AI model, you will use variables to hold the AI's response, data types to know whether you got text or a number back, `if/else` to check whether the response passed validation, and `for` loops to process multiple AI responses one at a time.

Master these four now and everything that follows will feel like combining familiar building blocks — not learning something new each time.

---

## Variables — Naming and Storing Values

**A variable is a named box in the computer's memory where you store a value.**

Think of it like a labelled container in a kitchen — the label is the variable name, and what is inside is the value. You do not need to know exactly where in memory it is stored — you just ask for it by name and Python gives you what is inside.

**Basic syntax:**

```python
age = 20
```

Symbol by symbol:
- `age` — the **variable name**. You choose this. It should describe what it holds
- `=` — the **assignment operator**. This does NOT mean "equals" the way it does in maths. It means "store the value on the right into the variable named on the left." Read it as "age is assigned 20"
- `20` — the **value** being stored

Once this line runs, you can use `age` anywhere later and Python will substitute in `20`.

**Variable naming rules:**
- Names are **case-sensitive** — `Age` and `age` are two different variables
- Use **descriptive names** — `student_score` is far better than `x`
- Use **lowercase with underscores** — `total_amount`, `is_valid`, `student_name` (this style is called snake_case)
- Cannot start with a number — `2name` is invalid, `name2` is fine
- Cannot use Python reserved words like `print`, `if`, `for` as variable names

**Variables can be reassigned — you can change the value stored in a variable:**

```python
score = 75
print(score)    # prints 75

score = 80      # reassign — the old value 75 is replaced
print(score)    # prints 80
```

The variable `score` now holds `80`. The old value `75` is gone. This is how programs update information as they run.

---

## Data Types — String, Integer, Float, Boolean

Every value stored in a variable has a **data type** — it tells Python what kind of value it is, and what operations are valid on it.

| Data Type | Python Name | What It Stores | Example |
|---|---|---|---|
| **String** | `str` | Text — any characters, wrapped in quotes | `name = "Alex"` |
| **Integer** | `int` | Whole numbers — no decimal point | `age = 20` |
| **Float** | `float` | Numbers with a decimal point | `price = 49.99` |
| **Boolean** | `bool` | Only two values — `True` or `False` | `is_student = True` |

You can check any variable's data type using `type()`:

```python
name = "Alex"
age = 20
price = 49.99
is_student = True

print(type(name))        # <class 'str'>
print(type(age))         # <class 'int'>
print(type(price))       # <class 'float'>
print(type(is_student))  # <class 'bool'>
```

### Working with Strings

Strings can be joined together using `+` — this is called **concatenation**:

```python
first_name = "Alex"
last_name = "Smith"
full_name = first_name + " " + last_name
print(full_name)    # Alex Smith
```

You can find the length of a string using `len()`:

```python
name = "Alex"
print(len(name))    # 4
```

`len()` is a built-in Python function that counts how many characters are in a string — or how many items are in a list (you will see this again in the for loops section).

### The Critical Difference — String vs Number

`age = 20` (an integer) and `age = "20"` (a string) look almost identical but behave completely differently:

```python
print(20 + 5)      # 25  — mathematical addition
print("20" + "5")  # 205 — text joined together, not added
```

`"20" + "5"` gives `"205"` — Python joins the two pieces of text. This is one of the most common beginner mistakes — mixing up a number with text that looks like a number. If you mean a number, never put quotes around it.

**What happens when you mix a string and a number:**

Every beginner hits this error. Knowing what it means before it happens means you will fix it in seconds instead of panicking:

```python
age = 20
print("You are " + age + " years old")
```

```
TypeError: can only concatenate str (not "int") to str
```

Python cannot join a string and an integer with `+` — they are different types. The fix is to convert the integer to a string first using `str()`:

```python
age = 20
print("You are " + str(age) + " years old")
```

```
You are 20 years old
```

`str(age)` converts the integer `20` into the string `"20"` so Python can join it with the surrounding text. Alternatively, the easiest fix is to just use `print()` with commas — which handles mixed types automatically:

```python
age = 20
print("You are", age, "years old")
```

```
You are 20 years old
```

---

## If / Else — Writing Decision Logic

An `if` statement lets your program **make a decision** — run one block of code if a condition is true, and a different block if it is false.

**Basic syntax:**

```python
amount = 6000

if amount > 5000:
    print("Transaction needs additional verification.")
else:
    print("Transaction approved.")
```

Symbol by symbol:
- `if` — a Python keyword that starts a conditional check
- `amount > 5000` — the **condition** being tested. `>` means "greater than." Python evaluates this and gets `True` or `False`
- `:` — required after every condition and after `else`. Tells Python "the indented block below belongs here"
- **Indentation** — the `print` line is pushed in by 4 spaces. This is not decoration — in Python, indentation is how the language knows which lines are "inside" the if block. Remove it and Python throws an error
- `else:` — its block runs only when the `if` condition was `False`

Since `6000 > 5000` is `True`, the output is:
```
Transaction needs additional verification.
```

### Adding More Conditions with elif

`elif` (short for "else if") lets you check additional conditions in sequence. Python checks each condition from top to bottom and runs the block for the **first one that is True**, then skips the rest.

**Why elif exists:** Sometimes you have more than two possible outcomes. Without elif, you would need to nest multiple if/else blocks inside each other — which quickly becomes hard to read. elif keeps the logic flat and readable.

```python
score = 72

if score >= 90:
    print("Grade: A")
elif score >= 75:
    print("Grade: B")
elif score >= 60:
    print("Grade: C")
elif score >= 40:
    print("Grade: D")
else:
    print("Grade: Fail")
```

`score` is `72`: `72 >= 90` is False, `72 >= 75` is False, `72 >= 60` is True — Python prints "Grade: C" and skips the rest.

```
Grade: C
```

### Nested If — Checking One Thing Inside Another

Sometimes you need to check a second condition only if the first one was already true. You can put an `if` inside another `if` — this is called a **nested if**:

```python
score = 72
is_submitted = True

if is_submitted:
    if score >= 40:
        print("Pass")
    else:
        print("Fail — score too low")
else:
    print("Fail — assignment not submitted")
```

Think of it like a two-stage door check. First you check if the assignment was submitted at all. Only if it was do you bother checking the score. If it was not submitted, you do not even need to look at the score.

> Use nested ifs sparingly — more than two levels deep starts to get very hard to read. When you find yourself nesting deeply, consider using `and` / `or` instead to keep the logic flat.

| Operator | Meaning | Example |
|---|---|---|
| `==` | Equal to — **two** equals signs | `score == 100` |
| `!=` | Not equal to | `status != "active"` |
| `>` | Greater than | `amount > 5000` |
| `<` | Less than | `age < 18` |
| `>=` | Greater than or equal to | `marks >= 40` |
| `<=` | Less than or equal to | `price <= 99.99` |

> **The most common beginner mistake:** Using `=` instead of `==` inside an if condition. `=` assigns a value. `==` compares two values. Python will not always catch this error — but your program will behave incorrectly.

### Combining Conditions — and / or

Real decisions often involve checking more than one thing at a time. Python has two keywords for this:

- `and` — both conditions must be True for the block to run
- `or` — at least one condition must be True for the block to run

**Real life example:** A student passes a course only if they scored at least 40 AND attended at least 75% of classes. Scoring high but never attending is a fail. Attending every class but scoring below 40 is also a fail. Both must be true:

```python
score = 72
attendance = 80

if score >= 40 and attendance >= 75:
    print("Pass — both conditions met")
else:
    print("Fail — one or both conditions not met")
```

```
Pass — both conditions met
```

**Using `or` — either condition is enough:**

A user gets a discount if they are a student OR if they have a loyalty card:

```python
is_student = True
has_loyalty_card = False

if is_student or has_loyalty_card:
    print("Discount applied")
else:
    print("No discount")
```

```
Discount applied
```

Even though `has_loyalty_card` is `False`, `is_student` is `True` — and with `or`, one True is enough.

**Combining and + or with brackets:**

```python
age = 25
is_student = True
has_voucher = False

if (age < 30 and is_student) or has_voucher:
    print("Eligible for offer")
```

Use brackets to make the order of checking clear — just like in maths, Python evaluates inside brackets first.

---

## For Loops — Repeating an Action Across a List

### Lists — a Quick Introduction

A **list** is an ordered collection of values, written inside square brackets `[ ]`, separated by commas:

```python
scores = [78, 45, 32, 91, 60]
```

`scores` holds five integers. Lists can hold any data type — strings, floats, booleans, or even a mix:

```python
names = ["Alex", "Maria", "James", "Priya"]    # a list of strings
prices = [9.99, 24.50, 5.00, 149.99]           # a list of floats
```

A list of strings works exactly the same way as a list of numbers — you can loop over it, check conditions on each item, and use `len()` to count how many items it contains:

```python
names = ["Alex", "Maria", "James"]
print(len(names))    # 3

for name in names:
    print("Hello,", name)
```

```
Hello, Alex
Hello, Maria
Hello, James
```

### The For Loop

A `for` loop repeats a block of code **once for every item in a list** — without you having to write that code out five separate times.

**Basic syntax:**

```python
scores = [78, 45, 32, 91, 60]

for score in scores:
    print(score)
```

Symbol by symbol:
- `for` and `in` — Python keywords meaning "for each item in this list, do the following"
- `score` — a **temporary variable** you choose. It holds one item from the list at a time. On the first pass it holds `78`, on the second `45`, and so on
- `scores` — the list being looped over
- `:` and indentation — exactly as with `if`, the colon and indented block define what repeats

Output:
```
78
45
32
91
60
```

### Computing a Total with a Loop

```python
scores = [78, 45, 32, 91, 60]
total = 0

for score in scores:
    total = total + score

average = total / len(scores)
print("Class average:", average)
```

Step by step:
- `total = 0` — an **accumulator variable** created before the loop starts. It must start at `0` so the first addition works
- `total = total + score` — on each pass, takes the current `total`, adds the current `score`, and stores the result back. After five passes: `78+45+32+91+60 = 306`
- `len(scores)` — counts how many items are in the list. Here it returns `5`
- `306 / 5 = 61.2`

Output:
```
Class average: 61.2
```

> **Important:** Always initialise accumulator variables **before** the loop — never inside it. If `total = 0` was inside the loop, it would reset to zero on every pass and you would never accumulate anything.

### The += Shorthand

`total = total + score` is so common in Python that there is a shorter way to write it:

```python
total += score    # exactly the same as: total = total + score
```

`+=` means "add the right side to the variable on the left and store the result back." You will see this constantly in real code — both versions work, but `+=` is what most developers write. The same shorthand exists for subtraction (`-=`), multiplication (`*=`), and division (`/=`):

```python
total += score     # total = total + score
total -= score     # total = total - score
total *= 2         # total = total * 2
total /= 5         # total = total / 5
```

### Using range() — Repeating a Fixed Number of Times

Sometimes you want to repeat something a fixed number of times rather than looping over a list. Python's built-in `range()` function generates a sequence of numbers for exactly this:

```python
for i in range(5):
    print("Step", i)
```

Output:
```
Step 0
Step 1
Step 2
Step 3
Step 4
```

`range(5)` generates the numbers 0, 1, 2, 3, 4 — five numbers starting from 0. This is extremely common in real code. You will see `for i in range(...)` constantly — whenever you need to repeat something a known number of times rather than iterate over a specific list.

```python
# Count from 1 to 5 instead of 0 to 4
for i in range(1, 6):
    print(i)
```

`range(1, 6)` starts at 1 and stops before 6 — giving you 1, 2, 3, 4, 5.

---

## Best Practices

- Use **meaningful variable names** — `total_price` is far clearer than `x`
- Always initialise **accumulator variables** before a loop, never inside it
- Keep **indentation consistent** — use 4 spaces everywhere. Mixing tabs and spaces causes hard-to-spot errors
- Add **comments** (`#`) to explain what a block of code is doing, especially inside loops and conditions

## Common Beginner Mistakes

- Using `=` instead of `==` inside an `if` condition — assignment vs comparison
- Forgetting the colon `:` after `if`, `elif`, `else`, or `for`
- Forgetting to indent the block under `if` or `for`
- Confusing `"20"` (a string) with `20` (an integer) — they behave very differently in calculations
- Initialising the accumulator variable inside the loop instead of before it

---

## Worked Example — Online Shopping Cart Checker

**Specification:** Given a list of item prices in a shopping cart, print whether each item is "Budget" (under $50) or "Premium" ($50 or above), then print the cart total.

```python
cart = [12.99, 75.00, 34.50, 120.00, 8.99]
total = 0

for price in cart:
    if price >= 50:
        print(price, "-> Premium item")
    else:
        print(price, "-> Budget item")
    total = total + price

print("Cart total: $", total)
```

**Expected output:**

```
12.99 -> Budget item
75.0 -> Premium item
34.5 -> Budget item
120.0 -> Premium item
8.99 -> Budget item
Cart total: $ 251.48
```

**Line-by-line explanation:**

- `cart = [12.99, 75.00, 34.50, 120.00, 8.99]` — a list of five floats (prices with decimal points)
- `total = 0` — accumulator variable, initialised before the loop
- `for price in cart:` — `price` takes each value in turn: `12.99`, then `75.00`, and so on
- `if price >= 50:` — `12.99 >= 50` is False → "Budget item". `75.00 >= 50` is True → "Premium item"
- `total = total + price` — runs on every pass, regardless of which branch the `if/else` took. It sits at the same indentation level as the `if`, so it is part of the `for` loop but not part of either branch
- The final `print` sits outside the loop (not indented under `for`) — it runs once, after all five items are processed

**Try it yourself:**
Add one more price to the cart list. Before running, predict which category it falls into and what the new total will be. Then run the code to check.

---

## Key Takeaways

- A **variable** is a named box that stores a value. `=` assigns a value — it does not mean mathematical equality
- Variables can be **reassigned** — the new value replaces the old one
- Python's four foundational data types: **string** (text), **integer** (whole numbers), **float** (decimal numbers), **boolean** (True/False)
- `"20"` (string) and `20` (integer) are not the same — mixing them with `+` throws a `TypeError`. Fix with `str()` or use `print()` with commas
- `and` requires both conditions to be True. `or` requires at least one to be True
- Nested `if` statements check a second condition inside a first one — use sparingly, keep logic flat where possible
- `if` / `elif` / `else` lets your program make decisions. Every condition line ends with `:` and its block must be indented
- `==` compares for equality. `=` assigns a value. Never confuse the two
- A **list** `[ ]` holds an ordered collection of values — strings, numbers, or any type
- A `for` loop repeats a block once for every item in a list
- `total += score` is shorthand for `total = total + score` — used constantly in real code
- `range(n)` generates numbers from 0 to n-1 — use it when you want to repeat something a fixed number of times
- **Accumulator variables** must be initialised before the loop — never inside it
- Indentation is not cosmetic — it is part of Python's grammar

> **Interview tip:** Be ready to trace through a short `for` / `if` program line by line, out loud, explaining what each line does and what the output will be before running it. This is one of the most common exercises in entry-level AI engineering interviews.

---

## Reference Links

- 📎 [Python Official Documentation — Data Structures](https://docs.python.org/3/tutorial/datastructures.html) — official reference on lists and operations
- 📎 [Python Official Documentation — Control Flow](https://docs.python.org/3/tutorial/controlflow.html) — official reference on if, elif, else, and for
- 📎 [W3Schools — Python Variables](https://www.w3schools.com/python/python_variables.asp) — beginner-friendly supplementary reading with interactive examples
- 📎 [Real Python — Python For Loops](https://realpython.com/python-for-loop/) — in-depth beginner guide to for loops including range()
