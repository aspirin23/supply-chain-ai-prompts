[← Back to Prompting Guide](../prompting-guide.md)

# Pattern 1 — Role Prompting

## What it is

Assigning the model a specific professional identity before asking your question. Instead of asking a generic assistant for help, you tell it exactly whose expertise, vocabulary, and judgment to adopt.

> *"You are a senior supply chain analyst specialising in CPG demand planning."*

## Why it works

A model without an assigned role defaults to a generic, broadly-helpful persona — calibrated to satisfy the widest possible audience. That's exactly the wrong calibration for operational work, where the right answer depends on who's asking and what they already know.

Assigning a role does three things at once:

- **Sets vocabulary** — a "senior procurement analyst" gets different terminology than a "junior buyer," without you having to specify a glossary.
- **Sets depth** — a role with seniority implied gets less hand-holding and more direct judgment calls; a role aimed at a generalist gets more explanation.
- **Sets the lens for ambiguity** — when a request is underspecified, the model resolves the gap in the direction the role would. A "reliability engineer" and a "finance director" asked the same vague question about a maintenance backlog will fill in the blanks differently, and a defined role tells the model which direction to lean.

This is the cheapest structural change you can make to a prompt — one sentence — and it's usually the single biggest jump in output quality for business users.

## When to use it

Almost always. Role prompting is close to a default-on pattern: there's rarely a reason *not* to specify a role, even for simple tasks. It becomes essential — not just helpful — when:

- The task requires domain judgment, not just data manipulation (e.g., assessing whether a delivery delay is "concerning" requires a role's threshold for concern)
- You need a specific vocabulary register (technical for an engineer, plain-language for an executive)
- The same underlying question needs different answers for different audiences

## Worked examples

### CPG & Retail

> *"You are a senior demand planner at a national grocery retailer, responsible for forecast accuracy across the fresh produce category. You are reviewing a forecast that significantly under-predicted demand for a promoted SKU last week. Identify the most likely drivers of the miss and what you'd check first before adjusting the forecast model."*

Without the role, a generic prompt asking "why did this forecast miss?" invites a textbook list of possible causes. With the role, the model prioritizes the checks a demand planner would actually run first — promotion lift assumptions, cannibalization from adjacent SKUs, weather sensitivity — in the order operational experience would suggest, not the order a statistics textbook would list them.

### Manufacturing

> *"You are a plant reliability engineer responsible for predictive maintenance on a fleet of CNC machines. A vibration sensor on Line 4 is showing a gradual upward trend over the past three weeks. Assess the risk and recommend next steps."*

A reliability engineer's threshold for "this needs action" is different from a data scientist's. The role tells the model to weigh the cost of unplanned downtime against the cost of a precautionary maintenance window — a judgment call specific to the role, not just a description of the trend.

### Energy & Utilities

> *"You are an energy procurement analyst at a large industrial utility, evaluating long-term power purchase agreement (PPA) bids. Review the attached bid terms and flag the contractual clauses that carry the most price or volume risk over a 10-year term."*

Without the role, the model treats this as a generic contract-review task and may flag legal boilerplate alongside genuine commercial risk indiscriminately. With the role, it weighs clauses the way a procurement analyst would — price escalation triggers, curtailment terms, force majeure scope — because those are the categories that matter to that specific job function.

## When this pattern fails

Role prompting is high-leverage but not magic. It commonly underperforms when:

- **The role is assigned but no context follows.** "You are a supply chain analyst. What should I do?" still produces a vague answer — the role narrows the lens, but it doesn't supply the situational facts the model needs. Role without context is necessary but not sufficient.
- **The role is too generic to differentiate anything.** "You are an expert" or "you are a professional" doesn't calibrate vocabulary or judgment in any specific direction — it needs to name a function, seniority, or specialization to do real work.
- **The task doesn't actually require judgment.** For pure data transformation (reformat this table, extract these fields), a role adds little — the task itself already fully specifies the output.
- **You assign a role that conflicts with the rest of the prompt.** Asking a model to act as a "CFO" while also asking for highly technical engineering detail creates an internal tension the model has to resolve on its own, often inconsistently.

## Combine with

Role prompting pairs especially well with [**Constraint setting**](./05-constraint-setting.md) — once you've told the model who it is, constraints let you sharpen *how* that persona communicates (tone, what to avoid, audience for the output). The two together get you most of the way to a finished, usable draft without needing few-shot examples at all.

## Quick template

```
You are a [specific job title], responsible for [specific area of ownership] 
at a [type of organisation/industry context].

[Then continue with your context, task, constraints, and output format as normal.]
```

---

[← Back to Prompting Guide](../prompting-guide.md) &nbsp;|&nbsp; [Next: Few-shot examples →](./02-few-shot-examples.md)
