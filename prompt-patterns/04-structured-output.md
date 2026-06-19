[← Back to Prompting Guide](../prompting-guide.md)

# Pattern 4 — Structured Output

## What it is

Explicitly specifying the format, structure, and length of the model's response, rather than letting it default to flowing prose.

> *"Return your analysis in the following format:*
> *- Summary (two sentences)*
> *- Key findings (bullet list, maximum five points)*
> *- Recommended actions (numbered list, one sentence each)*
> *- Risks and assumptions (bullet list)"*

## Why it works

Left unspecified, a model's default output shape is a well-organised paragraph or two — because that's the most common shape for general writing, and absent other signals, that's what it produces. Business work, though, is rarely consumed as a paragraph. It's pasted into a slide, dropped into a table, scanned in a dashboard, or read by someone who needs the bottom line in the first five seconds.

Specifying structure upfront does two things that fixing the format *after the fact* can't:

- **It changes what the model includes, not just how it's laid out.** A model asked for "a summary" with no structure tends to blend findings and recommendations together in narrative form. The same request with an explicit "Findings / Recommendations / Risks" structure forces a cleaner separation of those categories *during generation* — you get better thinking, not just better formatting, because the structure acts as a checklist the model has to satisfy.
- **It removes a full editing pass.** An unstructured paragraph that contains the right information still has to be manually reshaped into a table or bullet list before it's usable. Specifying the structure upfront means the first draft is close to the final shape.

This is also the pattern most directly tied to *where the output is going*. The right structure is determined by the destination — a Slack update, a board deck, a JSON payload for a downstream tool — not by what reads most naturally as prose.

## When to use it

Reach for structured output whenever:

- The output needs to slot directly into something else — a report section, an email, a slide, a dashboard field — without reformatting
- You're comparing multiple items (SKUs, suppliers, assets) and want them in a consistent, scannable shape rather than separate paragraphs
- You're feeding the output into another tool or system, in which case you can ask for markdown tables, JSON, or CSV-style output directly
- Different parts of the answer serve different purposes (a finding vs. a recommendation vs. a caveat) and blending them into prose would bury the distinction

## Worked examples

### CPG & Retail

> *"Return your analysis of this week's replenishment exceptions in the following structure:*
> *- Headline (one sentence: how many SKUs at risk, total exposure)*
> *- Table: SKU | Current days of cover | Target | Likely driver | Recommended action*
> *- Watch list (bullet list: SKUs trending toward exception status but not yet critical)"*

This structure mirrors exactly how the output will be consumed — the headline for someone skimming in a status meeting, the table for someone working the exceptions directly, the watch list for someone planning next week. A prose paragraph covering the same ground would force the reader to extract all three uses themselves.

### Manufacturing

> *"Summarise the predictive maintenance alerts from this week in this structure:*
> *- Critical (table: Asset | Issue | Days until recommended action | Confidence)*
> *- Monitor (table: same columns, lower urgency)*
> *- Summary line: total assets flagged, total estimated downtime risk if no action taken"*

Splitting "Critical" from "Monitor" as separate tables — rather than one table with a severity column — means a reliability lead can scan the Critical table alone in a morning standup without reading past it to find what matters. The structure does triage work that a single flat list wouldn't.

### Energy & Utilities

> *"Return the load forecast deviation analysis in this format:*
> *- Executive summary (2–3 sentences, for the operations director)*
> *- Deviation table: Region | Forecast | Actual | % Deviation | Driver*
> *- Grid impact assessment (bullet list: reserve margin status, any curtailment risk)*
> *- Recommended monitoring actions (numbered list)"*

Naming the audience for the executive summary ("for the operations director") inside the structure spec — not just the format — keeps that section appropriately high-level even while the table beneath it stays detailed. The structure carries some of the audience-calibration work that would otherwise need to be stated separately.

## When this pattern fails

- **Over-specifying structure for a task that's genuinely exploratory.** If you're asking the model to think through an ambiguous problem with you, forcing it into a rigid table too early can flatten useful nuance into cells that don't fit it. Structure works best once you know what shape the answer should take — for open-ended exploration, let it think in prose first, then ask for the structured version once you know what you're looking for.
- **Specifying a structure that doesn't match the actual content.** A forced "Risks" section on a task with no real risks produces a filler bullet just to satisfy the template — watch for the model padding sections to match a structure you imposed, and relax the structure if a section consistently comes up empty.
- **Asking for structure without also controlling length.** "Bullet list of key findings" with no cap can produce twelve bullets when you wanted four. Pair structure with explicit limits (max five points, two sentences each) to get genuinely scannable output rather than just reformatted verbosity.
- **Using free-form prose structure descriptions instead of showing the shape.** Describing a table in a sentence ("include a table with SKU, days of cover, and action") works, but is more error-prone than literally sketching the column headers — the more visually explicit the spec, the more reliably the model reproduces it exactly.

## Combine with

Structured output pairs naturally with [**Few-shot examples**](./02-few-shot-examples.md) — when the structure is simple (a table, a numbered list), stating it explicitly is usually enough. When the structure is more nuanced or stylistic than column headers can capture, showing one fully worked example alongside the explicit structure removes any ambiguity that's left.

## Quick template

```
Return your response in the following structure:

- [Section 1 name] ([length/format constraint])
- [Section 2 name] ([length/format constraint])
- [Table, if needed: Column A | Column B | Column C]
- [Section 3 name] ([length/format constraint])

[State any overall length cap or formatting rule that applies across all sections.]
```

---

[← Previous: Chain of thought](./03-chain-of-thought.md) &nbsp;|&nbsp; [Back to Prompting Guide](../prompting-guide.md) &nbsp;|&nbsp; [Next: Constraint setting →](./05-constraint-setting.md)
