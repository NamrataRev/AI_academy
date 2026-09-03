# Topic 2: The 5-Role Context Framework

---

## Moving from Basic to Advanced Prompting

In Topic 1, you learned the individual building blocks of prompt engineering: assigning roles, providing few-shot examples, enforcing constraints, using chain-of-thought, and controlling output formats. 

While you can use these techniques individually, enterprise-grade AI applications require a structured approach to combining them. This is where **The 5-Role Context Framework** comes in. It is a systematic way to construct highly robust, reliable system prompts by ensuring five critical elements of context are present.

The 5 roles of a complete context are:
1. **Authority** (Who is speaking?)
2. **Exemplar** (What does good look like?)
3. **Constraint** (What are the strict boundaries?)
4. **Rubric** (How is success evaluated?)
5. **Metadata** (What is the surrounding context/data?)

Let's break down each role.

---

## 1. Authority (The Persona)

**Authority** establishes the identity, expertise level, and tone of the AI. It dictates *who* the model should emulate.

If an AI lacks Authority, it defaults to a generic, overly helpful, and sometimes robotic tone. By explicitly assigning Authority, you focus the model's vocabulary and reasoning patterns.

**Example:**
> "You are a Senior Data Scientist specializing in financial fraud detection with 15 years of experience. You communicate in a direct, highly technical, and academic tone."

## 2. Exemplar (The Pattern)

**Exemplars** are your few-shot examples. They show the AI the exact pattern it needs to follow, reducing the need for lengthy, ambiguous instructions. 

In a robust framework, Exemplars don't just show the final answer; they show the *expected input* mapped to the *expected output*, including the formatting (like JSON).

**Example:**
> "Example 1: 
> Input: 'User logged in from 3 different countries in 1 hour.' 
> Output: `{"risk_level": "HIGH", "reason": "Impossible travel velocity"}`"

## 3. Constraint (The Boundaries)

**Constraints** define what the model *must not do* or strictly *must do*. They are the guardrails of your application. Constraints prevent the AI from hallucinating features, breaking JSON schemas with conversational filler, or discussing off-limit topics.

**Example:**
> "CRITICAL CONSTRAINTS: 
> 1. You must output ONLY raw JSON. 
> 2. Do not include markdown block tags like ```json.
> 3. Under no circumstances should you recommend freezing a bank account without human approval."

## 4. Rubric (The Evaluation Criteria)

A **Rubric** tells the AI exactly how its work will be judged. Just like grading a student, if you give the AI a rubric, it will attempt to optimize its answer to score perfectly against those specific criteria. This is particularly useful for tasks involving reasoning, summarizing, or creative writing.

**Example:**
> "Your output will be evaluated on the following criteria:
> - Accuracy: Did you correctly identify all fraudulent indicators?
> - Conciseness: Is the explanation under 50 words?
> - Actionability: Did you provide a clear next step for the security team?"

## 5. Metadata (The Environment)

**Metadata** provides the AI with the situational awareness it needs to answer correctly. This includes the current date, the user's location, database schemas, or definitions of internal company acronyms. Without Metadata, the AI might give an answer that is technically correct but practically useless for your specific system.

**Example:**
> "METADATA: 
> - Current Date: October 15, 2024
> - Internal System: The fraud database is called 'WatchTower'.
> - User Tier: Enterprise Customer"

---

## Bringing it All Together in Python

Here is how you combine the 5-Role Context Framework into a single, production-ready System Prompt using the Anthropic API.

```python
import anthropic
import json

def analyze_fraud_risk(transaction_log, api_key):
    client = anthropic.Anthropic(api_key=api_key)
    
    # The 5-Role Context Framework System Prompt
    system_prompt = """
    <authority>
    You are a Senior Financial Security Analyst. You are highly analytical, objective, and output strictly structured data.
    </authority>
    
    <metadata>
    Current Date: 2024-10-15
    Internal Alert System: 'WatchTower'
    Risk Thresholds: Transactions over $10,000 require manual review.
    </metadata>
    
    <rubric>
    Your analysis will be judged on:
    1. Strict adherence to the JSON schema.
    2. Correct identification of impossible travel or unusual volume.
    3. Providing a concise, 1-sentence explanation.
    </rubric>
    
    <constraints>
    1. Output ONLY valid JSON.
    2. Do not include introductory or concluding text.
    3. Never recommend automatic account termination.
    </constraints>
    
    <exemplars>
    Example 1:
    Input: "User JohnD spent $5 at Starbucks in NY at 8:00 AM, then $500 at a BestBuy in London at 8:30 AM."
    Output: {"risk_level": "HIGH", "flag": "Impossible travel", "action": "Send to WatchTower"}
    </exemplars>
    """
    
    try:
        response = client.messages.create(
            model="claude-3-5-sonnet-20240620",
            max_tokens=200,
            system=system_prompt,
            messages=[{"role": "user", "content": f"Analyze this log: {transaction_log}"}]
        )
        
        # Parse the output
        return json.loads(response.content[0].text)
        
    except json.JSONDecodeError:
        return {"error": "Failed to parse AI output as JSON."}
    except Exception as e:
        return {"error": str(e)}

# Test it
# log = "User Sarah22 spent $12,000 on electronics in Miami at 2 PM today."
# print(analyze_fraud_risk(log, "your-key-here"))
```

---

## Interview Questions

**Q1: "What is the 5-Role Context Framework in prompt engineering?"**
A: It is a structured methodology for writing system prompts by defining five key elements: Authority (persona), Exemplar (examples), Constraint (boundaries), Rubric (evaluation criteria), and Metadata (situational context). 

**Q2: "Why is 'Metadata' important when calling an LLM programmatically?"**
A: LLMs only know the data they were trained on, which has a cutoff date and lacks knowledge of your specific internal company systems. Injecting Metadata (like current dates, user preferences, or database schemas) gives the model the situational awareness needed to provide a relevant, system-specific answer.

---

## Quick Recap

To write enterprise-grade prompts, ensure your prompt covers the 5 Roles:
- **Authority:** Who is the AI?
- **Exemplar:** Give examples of the input/output pattern.
- **Constraint:** Set strict rules on what the AI cannot do.
- **Rubric:** Tell the AI how it will be judged.
- **Metadata:** Provide the contextual data necessary to solve the problem.
- Using XML tags (like `<constraints>`) is an excellent way to cleanly organize these 5 roles within your system prompt.
