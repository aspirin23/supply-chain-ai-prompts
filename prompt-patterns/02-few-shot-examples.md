[← Back to Prompting Guide](../prompting-guide.md)

# Pattern 2 — Few-Shot Examples

## What it is

Showing the model one or more examples of the output you want before asking it to produce its own. Instead of describing the format, tone, and depth in the abstract, you demonstrate it once and let the model pattern-match against your example.

> *"Here is an example of how I want exceptions summarised: [example]. Now apply the same format to the following exceptions: [data]"*

## Why it works

Language is a lossy way to describe format. You can write three sentences trying to describe "concise but not too brief, professional but not stiff, with the SKU number leading and the action item at the end" — or you can show one example and the model absorbs all of that at once, including things you didn't think to specify.

Few-shot examples work because they communicate several things simultaneously that are hard to separate into instructions:

- **Length and density** — how much detail per point, how long is "concise" in practice
- **Tone** — formal vs. conversational, hedged vs. direct
- **Implicit structure** — what comes first, what's optional, what's always included
- **The boundary of "good enough"** — an example sets a quality bar the model will try to match, not just a format to fill in

This is also why few-shot is the fastest way to fix a recurring formatting complaint. If you keep getting outputs that are "close but not quite right," an instruction tweak often doesn't fully close the gap — an example usually does, because it removes the ambiguity in your wording rather than adding more wording on top of it.

## When to use it

Reach for few-shot examples when:

- You've already tried describing the format in words and the output still isn't landing
- The output needs to match an existing house style — a report template, a recurring email format, a specific way your team writes exception summaries
- Tone is doing a lot of work (e.g., "professional but not alarmist" is much easier to show than to define)
- You need consistency across many similar items (a batch of SKU exceptions, a list of supplier risk flags) and want every entry to look like it came from the same person

## Worked examples

### CPG & Retail

> *"Here is an example of how I want stockout risk flagged for the weekly category review:*
>
> *SKU 48217 — Greek yogurt, 4-pack. Days of cover: 2.1 (target: 7). Driver: in-store promotion drove 3x normal velocity, base forecast not adjusted. Action: expedite replenishment from DC3, flag for promo-forecast recalibration next cycle.*
>
> *Now apply the same format to these five SKUs: [data]"*

The example does work that a paragraph of instructions would struggle to: it shows that the driver should be a single causal sentence (not a list of possibilities), that the action should be split into immediate + systemic, and that DC-level specificity is expected. A planner reading the output would recognise the house style instantly.

### Manufacturing

> *"Here is the format our reliability team uses for sensor anomaly write-ups:*
>
> *Line 4, Spindle Motor — Vibration trending up 18% over 3 weeks, currently within tolerance but accelerating. Comparable pattern preceded bearing failure on Line 2 in March. Recommend inspection within 5 operating days; do not wait for scheduled PM.*
>
> *Write up the following three anomalies in the same format: [sensor data]"*

This example carries information that's nearly impossible to instruct around cleanly — specifically, that citing a comparable historical incident is expected practice and that the recommendation should state urgency relative to the existing maintenance schedule, not just "should be inspected."

### Energy & Utilities

> *"Here is how we summarise load forecast deviations for the operations briefing:*
>
> *Region: North grid, Tuesday peak. Actual demand exceeded forecast by 6.2%. Likely driver: unforecasted temperature spike (actual 34°C vs. forecast 29°C). Grid impact: within reserve margin, no curtailment required. Watch item: repeat pattern would erode reserve margin by Thursday.*
>
> *Summarise the following three deviations in the same format: [data]"*

The example demonstrates a specific discipline — every write-up ends with a forward-looking "watch item," not just a backward-looking explanation. That's a house convention that would take several sentences to instruct explicitly, and even then might not transfer as reliably as showing it once.

## When this pattern fails

- **The example is too narrow.** A single example drawn from an unusual edge case will get over-fitted — the model may replicate quirks specific to that one example rather than the general pattern you intended. Two examples spanning slightly different scenarios is often safer than one.
- **The example conflicts with your written instructions.** If your text says "keep it under three sentences" but your example is five sentences long, the model has to guess which one to trust — and it doesn't always pick the one you'd want.
- **You're using few-shot for a task that's actually about reasoning, not format.** Showing an example of a *conclusion* doesn't teach the model your *reasoning process* — for that, you want chain of thought, not few-shot.
- **The data in your example is too memorable.** If your example uses a real, distinctive SKU or supplier name, the model can sometimes latch onto the specific entity rather than the structural pattern. Genericise example data where you can.

## Combine with

Few-shot examples pair naturally with [**Structured output**](./04-structured-output.md) — an example *is* a structured output specification, just shown rather than described. When the structure is simple, stating it explicitly is often enough; when the structure is nuanced or stylistic, showing one worked example alongside the explicit structure removes any remaining ambiguity.

## Quick template

```
Here is an example of the output format I want:

[One worked example, in full, exactly as you'd want it to look]

Now apply the same format to the following: [your actual data/task]
```

---

[← Previous: Role prompting](./01-role-prompting.md) &nbsp;|&nbsp; [Back to Prompting Guide](../prompting-guide.md) &nbsp;|&nbsp; [Next: Chain of thought →](./03-chain-of-thought.md)
