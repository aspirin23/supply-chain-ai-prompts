[← Back to Prompting Guide](../prompting-guide.md)

# Pattern 3 — Chain of Thought

## What it is

Asking the model to reason step by step before arriving at a conclusion, rather than jumping straight to a final answer.

> *"Think through this step by step. First, identify what the data tells us about demand variability for this SKU. Then assess whether current safety stock levels are appropriate given that variability. Finally, recommend an adjustment and explain your reasoning."*

## Why it works

When a model is asked for a conclusion directly, it has to produce the right answer in one pass — there's no intermediate space to catch a faulty assumption before it propagates into the final output. Asking it to reason step by step changes the shape of the task: each step's output becomes an input to the next, which means errors are more likely to surface mid-reasoning, where you can see them, rather than being baked silently into a confident-sounding conclusion.

There's a second, equally important benefit that's easy to overlook: **auditability**. In operational contexts, you often care as much about *why* an answer was reached as the answer itself — because you're the one who has to defend the recommendation to a stakeholder, or because you need to know which assumption to double-check before acting on it. A conclusion with no visible reasoning is a black box; a conclusion with visible steps is something you can sanity-check against your own judgment and stop trusting at the exact point where it stops making sense.

This is also where chain of thought earns its cost. It produces longer output and takes longer to read than a direct answer — that overhead is worth paying when the task is non-trivial and the stakes of an unexamined error are real.

## When to use it

Reach for chain of thought when:

- The task involves multiple dependent judgments (assess variability → then assess if current policy is adequate → then recommend a change) rather than a single lookup or classification
- You need to *trust and verify* the reasoning, not just consume the conclusion — for decisions you'll be accountable for
- The "obvious" answer might be wrong for a non-obvious reason, and you want the model to surface that reason rather than skip past it
- You're debugging why the model's conclusions don't match your own intuition — seeing the steps shows you exactly where the divergence happens

## Worked examples

### CPG & Retail

> *"A promoted SKU sold through 40% faster than forecast last week. Think through this step by step: First, assess whether this looks like a forecasting model issue or a one-off promotional effect. Second, check whether comparable SKUs in the same promotion saw similar uplift. Third, based on that, recommend whether the base forecast needs recalibrating or whether this was a contained, promotion-specific event. Show your reasoning at each step."*

Without chain of thought, the model might jump straight to "recalibrate the forecast" — a plausible-sounding but potentially wrong conclusion if the uplift was actually contained to this one promotion. Walking through the comparable-SKU check first surfaces the evidence needed to make that call correctly, and you can see exactly which evidence tipped the recommendation.

### Manufacturing

> *"We're deciding whether to schedule unplanned downtime for Line 4 based on a vibration trend. Think step by step: First, assess how the current trend compares to the pattern that preceded the Line 2 bearing failure in March. Second, estimate the cost of unplanned downtime now versus the risk of running to scheduled maintenance in 9 days. Third, make a recommendation and state your confidence level."*

The step-by-step structure forces the comparison to the historical Line 2 incident to happen explicitly, rather than being silently assumed or silently ignored. If a reliability engineer disagrees with the final recommendation, they can pinpoint exactly which step they'd argue with — the pattern comparison, the cost estimate, or the threshold for acting on it.

### Energy & Utilities

> *"We're evaluating whether a 10-year PPA bid's price escalation clause is acceptable. Think through this step by step: First, calculate the cumulative price impact of the escalation clause over the contract term under a moderate inflation scenario. Second, compare that to the escalation terms in our two most recent comparable contracts. Third, assess whether the clause is in line with market norms or an outlier. Finally, give a recommendation."*

Procurement decisions like this are exactly where unexamined conclusions are risky — a flat "this clause looks fine" is not defensible to a contract review committee, but a conclusion built on a visible calculation and a visible comparison to recent contracts is. The chain of thought *is* the work product here, not just a means to the final recommendation.

## When this pattern fails

- **Applied to simple, single-step tasks.** Asking a model to "think step by step" before extracting a date from a paragraph just adds length without adding accuracy — there's no chain to walk because there's no real intermediate reasoning to expose.
- **The steps you specify don't actually match how the problem should be reasoned through.** If you prescribe a three-step sequence that skips a step a real analyst would consider essential, the model will follow your sequence faithfully and miss what you missed — chain of thought structures the reasoning you ask for, it doesn't add reasoning you didn't ask for.
- **Mistaking visible steps for correct steps.** A model can produce confident, well-structured intermediate reasoning that is still wrong at one step — the visibility makes errors *easier to catch*, it doesn't make them disappear. Chain of thought output still needs review, especially at the step where a judgment call (not just a calculation) is being made.
- **Using it as a substitute for giving the model real data.** No amount of step-by-step reasoning compensates for the model not having the actual numbers — it will reason fluently and plausibly over assumptions if you haven't given it data to reason over instead.

## Combine with

Chain of thought pairs well with [**Role prompting**](./01-role-prompting.md) — the role determines *what a good reasoning path looks like* for this task (a reliability engineer and a finance analyst would walk through the same vibration data differently), so defining the role before asking for step-by-step reasoning keeps the steps themselves relevant to the right kind of judgment.

## Quick template

```
[Your role and context as normal]

Think through this step by step:
First, [first sub-judgment or check].
Then, [second sub-judgment, building on the first].
Finally, [the conclusion or recommendation, with reasoning stated].

Show your reasoning at each step before giving the final answer.
```

---

[← Previous: Few-shot examples](./02-few-shot-examples.md) &nbsp;|&nbsp; [Back to Prompting Guide](../prompting-guide.md) &nbsp;|&nbsp; [Next: Structured output →](./04-structured-output.md)
