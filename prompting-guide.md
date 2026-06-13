# Prompting Guide for Supply Chain Professionals

### *"Summarise the supplier report."* vs a 60-word prompt that produces a board-ready analysis in one shot. The gap between those two is what this guide covers.

A practical framework for getting useful outputs from LLMs — written for planners, analysts, and operations professionals.  
By the end you will have a reusable prompt structure and five patterns you can apply to your next supply chain problem today.  
*(15 minute read)*

---

## Contents

1. [Why prompt structure matters](#1-why-prompt-structure-matters)<br>&nbsp;&nbsp;&nbsp;&nbsp;*Why vague inputs produce vague outputs — and how to fix it in under a minute*
2. [The core framework](#2-the-core-framework)<br>&nbsp;&nbsp;&nbsp;&nbsp;*A five-component structure you can apply to any business problem*<br>&nbsp;&nbsp;&nbsp;&nbsp;*Includes a ready-to-use template* → [Jump to the reusable template](#the-reusable-template) *(copy and customize)*
3. [The five most useful patterns for business](#3-the-five-most-useful-patterns-for-business)<br>&nbsp;&nbsp;&nbsp;&nbsp;*The techniques that consistently produce better results in operational contexts*<br>&nbsp;&nbsp;&nbsp;&nbsp;— [Role prompting](#pattern-1--role-prompting)<br>&nbsp;&nbsp;&nbsp;&nbsp;— [Few-shot examples](#pattern-2--few-shot-examples)<br>&nbsp;&nbsp;&nbsp;&nbsp;— [Chain of thought](#pattern-3--chain-of-thought)<br>&nbsp;&nbsp;&nbsp;&nbsp;— [Structured output](#pattern-4--structured-output)<br>&nbsp;&nbsp;&nbsp;&nbsp;— [Constraint setting](#pattern-5--constraint-setting)
4. [Common mistakes and how to fix them](#4-common-mistakes-and-how-to-fix-them)<br>&nbsp;&nbsp;&nbsp;&nbsp;*The five things business users get wrong — with before/after fixes*
5. [How to read the prompts in this library](#5-how-to-read-the-prompts-in-this-library)<br>&nbsp;&nbsp;&nbsp;&nbsp;*Where to go next based on your industry*

---

## 1. Why prompt structure matters

An LLM doesn't know who you are, what you do, or what a good answer looks like for your context. It only knows what you tell it in the prompt.

When you type something vague — "summarise this supplier report" — the model makes assumptions. It assumes a generic reader, a generic purpose, and a generic format. The output you get back is usually technically correct and operationally useless.

This is not a model problem. It's a framing problem.

The way an LLM processes your input is closer to a very well-read analyst on their first day than a system that already understands your business. It has broad knowledge but no context about your role, your data, your constraints, or what you're going to do with the output. Your job as the prompter is to close that gap before the model starts generating.

The good news: you don't need to be a developer to do this well. You need a repeatable structure and an understanding of a few key patterns. That's what this guide covers.

---

## 2. The core framework

Every effective business prompt has five components. You don't always need all five — but knowing each one and when to use it is the foundation of good prompting.

```
Role → Context → Task → Constraints → Output format
```

### Role
Tell the model who it is playing. This sets the lens through which it interprets everything else.

> *"You are a senior supply chain analyst specialising in CPG demand planning."*

Without a role, the model defaults to a generic helpful assistant. With a role, it calibrates vocabulary, assumptions, and depth to match the persona you've defined.

### Context
Give the model the situational information it needs to respond usefully. Think of this as the briefing you'd give a consultant before asking them a question.

> *"We are reviewing weekly replenishment exceptions for a mid-size grocery retailer. The data covers 12 distribution centres across the UK. Service level targets are 98.5%."*

Context is where most business users underinvest. The more specific and operational your context, the more specific and operational your output.

### Task
State clearly what you want the model to do. Use an action verb. Be specific about the scope.

> *"Identify the top five categories driving the largest replenishment exceptions this week and suggest likely root causes for each."*

Avoid open-ended tasks like "analyse this" or "tell me about this." The model will answer — but not necessarily in the way that's useful to you.

### Constraints
Tell the model what to avoid, what to assume, and what limits apply. This is especially important in business contexts where tone, confidentiality, or output scope matters.

> *"Do not speculate beyond the data provided. Flag where assumptions are being made. Avoid technical jargon — the output will be shared with commercial stakeholders."*

Constraints reduce the gap between what the model thinks is helpful and what is actually useful in your context.

### Output format
Specify how you want the answer structured. Table, bullet list, executive summary, email draft, slide talking points — be explicit.

> *"Structure the output as a brief executive summary (three to four sentences) followed by a bullet list of findings, one per category."*

If you don't specify a format, the model will choose one. It may not be the format you needed.

---

### Putting it together

Here is the same request — weak and strong:

**Weak:**
> *"Summarise the supplier performance data."*

**Strong:**
> *"You are a supply chain analyst preparing a monthly supplier review for a manufacturing business. I will paste in raw supplier performance data covering on-time delivery, quality rejection rates, and lead time variance for the past quarter. Identify the three suppliers with the most significant performance deterioration and summarise the key issues for each. Focus on trends, not just single-period results. Avoid technical statistical language — this summary will be presented to procurement leadership. Structure the output as three short paragraphs, one per supplier, each no longer than five sentences."*

The strong version takes 30 seconds longer to write and produces an output that is ready to use.

---

### The reusable template

Use this as your starting point for any new prompt. Fill in the components that are relevant, leave out the ones that aren't.

```
ROLE:
You are a [job title / expert persona] with experience in [domain or industry].

CONTEXT:
[Describe the business situation, the data you are working with, and any relevant background the model needs to understand your problem.]

TASK:
[State clearly what you want the model to do. Start with an action verb — analyse, summarise, identify, draft, compare, recommend.]

CONSTRAINTS:
[Optional: specify what to avoid, what to assume, tone requirements, confidentiality limits, or scope boundaries.]

OUTPUT FORMAT:
[Specify how you want the response structured — table, bullet list, short paragraphs, executive summary, numbered recommendations, etc.]
```

> **Note:** You do not need all five components every time. A simple task with clear context may only need two or three. The framework is a checklist, not a rigid script — use it flexibly and add components only where they add clarity. As a rule of thumb: the higher the stakes or the more complex the task, the more components you should include.

---

## 3. The five most useful patterns for business

Beyond the core framework, a handful of prompting patterns consistently produce better results in operational and enterprise contexts.

---

### Pattern 1 — Role prompting

**What it is:** Assigning the model a specific professional identity before asking your question.

**Why it works:** The model adjusts its assumptions, vocabulary, and depth based on the role you define. A prompt written for a "logistics analyst" produces a different response than the same prompt written for a "CFO" — even if the underlying question is identical.

**When to use it:** Almost always. Role prompting is the single highest-leverage change most business users can make to their prompts.

**Example:**
> *"You are an experienced energy procurement analyst at a large utilities company. Your role is to help evaluate supplier bids and identify risk factors in long-term energy contracts."*

---

### Pattern 2 — Few-shot examples

**What it is:** Showing the model one or more examples of the output you want before asking it to produce its own.

**Why it works:** Examples communicate format, tone, and depth far more efficiently than instructions alone. The model pattern-matches against your examples rather than interpreting abstract descriptions.

**When to use it:** When you need output in a very specific format, at a specific length, or in a particular tone — and describing it in words alone is not working.

**Example:**
> *"Here is an example of how I want exceptions summarised:*
>
> *SKU 10234 — Replenishment exception: stock on hand fell to 3 days cover against a target of 14 days. Likely cause: promotional uplift not reflected in the base forecast. Recommended action: emergency replenishment order and forecast recalibration.*
>
> *Now apply the same format to the following exceptions: [paste data]"*

---

### Pattern 3 — Chain of thought

**What it is:** Asking the model to show its reasoning step by step before arriving at a conclusion.

**Why it works:** For analytical or multi-step problems, forcing the model to reason explicitly reduces errors and makes the logic auditable. It also helps you spot where the model's assumptions diverge from yours.

**When to use it:** Complex analytical tasks, root cause analysis, scenario evaluation, or any situation where you need to trust — and verify — the reasoning, not just the conclusion.

**Example:**
> *"Think through this step by step. First, identify what the data tells us about demand variability for this SKU. Then assess whether current safety stock levels are appropriate given that variability. Finally, recommend an adjustment and explain your reasoning."*

Or simply add:
> *"Think step by step before giving your final answer."*

---

### Pattern 4 — Structured output

**What it is:** Explicitly specifying the format, structure, and length of the model's response.

**Why it works:** LLMs default to flowing prose. In business contexts you almost always need something more structured — a table, a list, a template, a report section. Specifying the structure upfront saves significant editing time.

**When to use it:** Whenever the output needs to slot into a presentation, report, email, or dashboard without heavy reformatting.

**Example:**
> *"Return your analysis in the following format:*
> *- Summary (two sentences)*
> *- Key findings (bullet list, maximum five points)*
> *- Recommended actions (numbered list, one sentence each)*
> *- Risks and assumptions (bullet list)*"*

You can also request output as a markdown table, JSON, or any other structured format if you are feeding the output into a tool or system.

---

### Pattern 5 — Constraint setting

**What it is:** Explicitly telling the model what not to do, what not to assume, and what limits to respect.

**Why it works:** Without constraints, the model fills gaps with its own assumptions — which may not match your context, audience, or requirements. Constraints reduce unwanted variation and keep outputs within scope.

**When to use it:** When audience, tone, confidentiality, or scope matters — which in business contexts is nearly always.

**Example:**
> *"Do not include information that was not in the data provided. If you are making an assumption, state it explicitly. Keep the tone factual and avoid speculative language. The output will be shared with external stakeholders so do not reference internal system names or cost figures."*

---

## 4. Common mistakes and how to fix them

These are the patterns that most consistently produce weak outputs in business and enterprise contexts.

---

### Mistake 1 — The vague task

**What it looks like:**
> *"Analyse this inventory report."*

**Why it fails:** The model doesn't know what kind of analysis you need, what decisions it's supporting, or what a useful output looks like for your context.

**Fix:**
> *"Review this inventory report and identify the top three SKUs at risk of stockout in the next 14 days based on current stock on hand and average daily sales. For each SKU, state the current days of cover and suggest an immediate action."*

---

### Mistake 2 — No role or context

**What it looks like:**
> *"Write a supplier performance summary."*

**Why it fails:** The model doesn't know who is writing, who is reading, what the supplier relationship is, or what the summary is for.

**Fix:**
> *"You are a procurement analyst at a manufacturing company. Write a supplier performance summary for our quarterly business review with a key packaging supplier. The audience is senior procurement leadership. Cover on-time delivery, quality rejection rate, and lead time consistency. Tone should be professional and direct."*

---

### Mistake 3 — Assuming the model knows your data

**What it looks like:**
> *"What's causing the forecast variance this month?"*

**Why it fails:** The model has no access to your data unless you paste it in. It will either refuse or — worse — fabricate a plausible-sounding answer.

**Fix:** Always paste the relevant data, metrics, or context directly into the prompt.
> *"Here is this month's forecast vs actuals by category: [paste data]. Based on this, identify which categories have the largest variance and suggest likely causes."*

---

### Mistake 4 — Asking for everything at once

**What it looks like:**
> *"Analyse our supply chain performance, identify risks, recommend improvements, and write a board summary."*

**Why it fails:** Multi-part tasks with no structure produce sprawling, unfocused outputs that are hard to use.

**Fix:** Break it into sequential prompts, or use structured output to separate the components clearly.
> *"Step 1: Analyse the supply chain performance data below and identify the top three risk areas. [data]*
> *Step 2 (after reviewing Step 1): Based on those risks, recommend one specific action for each.*
> *Step 3: Draft a two-paragraph board summary covering the risks and recommended actions."*

---

### Mistake 5 — Not specifying the audience

**What it looks like:**
> *"Summarise the demand planning exceptions."*

**Why it fails:** A summary written for a demand planner looks very different from one written for a commercial director or a supply chain VP. Without specifying the audience, the model defaults to a generic middle ground that works for no one.

**Fix:**
> *"Summarise the demand planning exceptions for a weekly S&OP meeting. The audience is commercial and supply chain directors — assume they understand the business context but not the technical detail of the planning system. Focus on business impact, not process detail."*

---

## 5. How to read the prompts in this library

Each industry folder in this repo contains prompts built using the framework and patterns described above. They are not templates to copy blindly — they are worked examples to learn from and adapt.

Every prompt in the library includes a **"Why this works"** section that maps the prompt back to the framework. Reading that section is how you move from using these prompts to writing your own.

**The folders:**

| Folder | What's inside |
|--------|---------------|
| [`cpg-retail/`](./cpg-retail/prompts.md) | Demand forecasting, promotion planning, inventory optimisation, replenishment |
| [`manufacturing/`](./manufacturing/prompts.md) | Production planning, supplier risk, quality control, maintenance |
| [`energy-utilities/`](./energy-utilities/prompts.md) | Load forecasting, asset performance, ESG reporting, energy procurement |
| [`general-supply-chain/`](./general-supply-chain/prompts.md) | S&OP, KPI analysis, stakeholder reporting, scenario planning |

**Suggested path:**

1. Read this guide once end to end
2. Pick the industry folder closest to your current work
3. Read two or three prompts alongside their "Why this works" explanation
4. Adapt one prompt to your own context and test it
5. Come back to the other patterns as your use cases evolve

The goal is not to give you prompts to copy. It is to give you a mental model that lets you write better prompts for any operational problem you face.

---

*Part of the [supply-chain-llm-guide](https://github.com/anindya/supply-chain-llm-guide) repository. New content added regularly — star the repo to follow along.*