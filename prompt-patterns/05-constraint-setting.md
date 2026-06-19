[← Back to Prompting Guide](../prompting-guide.md)

# Pattern 5 — Constraint Setting

## What it is

Telling the model what not to do, what not to assume, and what limits to respect — explicitly, rather than hoping the right boundaries are implied by everything else in the prompt.

> *"Do not speculate beyond the data provided. Flag where assumptions are being made. Avoid technical jargon — the output will be shared with commercial stakeholders."*

## Why it works

A model without explicit constraints doesn't sit still and wait for guidance on edge cases — it fills the gap. Asked to summarise a dataset with a missing value, it might silently estimate. Asked to write for an unspecified audience, it picks a generic middle ground. Asked to be helpful, it sometimes adds context, caveats, or suggestions you didn't ask for and don't want in the final output.

None of that is the model malfunctioning — it's doing what "be helpful" defaults to when nothing has told it otherwise. Constraints are how you redirect that default behaviour toward what's actually useful in *your* context:

- **They close the gap between "plausible" and "correct."** A model filling in a gap with a reasonable-sounding assumption is often invisible in the output — it reads just as confidently as a grounded statement. A constraint like "flag any assumption explicitly" doesn't stop the model from needing to make assumptions sometimes, but it stops them from being silent.
- **They protect scope.** Business outputs often need to stay within a boundary — don't reference internal system names, don't include cost figures in an external-facing doc, don't go beyond what the data shows. Without stating this, "helpful" can mean "more than you wanted to share."
- **They calibrate tone and register**, especially when the audience for the output is different from the audience for the conversation itself — you might be technical, but the output needs to not be.

Constraints are the cheapest insurance in this whole framework: a sentence or two that prevents the most common ways a technically-correct output ends up being the wrong output for where it's headed.

## When to use it

Reach for constraint setting whenever:

- The output is going to an audience who didn't see the source data or the conversation that produced it — they only see the final draft, so anything unstated needs to be made explicit
- Confidentiality or scope genuinely matters — internal figures, system names, or sensitive specifics that shouldn't leak into an external-facing summary
- You've noticed the model tends to add unrequested padding (caveats, suggestions, "I hope this helps" framing) that doesn't belong in the final output
- Precision matters more than completeness — you'd rather the model say "the data doesn't show this" than guess

## Worked examples

### CPG & Retail

> *"Summarise this week's promotion performance for the regional VP update. Do not include SKU-level detail — aggregate to category level only. Do not speculate about causes beyond what the sell-through data shows; if a category's performance looks unusual, flag it as 'worth investigating' rather than offering a guess. Keep the tone factual, no celebratory language even where performance was strong."*

Without the constraints, a model might naturally want to explain *why* a category overperformed — which, absent real root-cause data, is exactly the kind of plausible-sounding speculation that shouldn't end up in a VP-facing update presented as fact.

### Manufacturing

> *"Draft the supplier quality summary for this quarter's business review. Do not include the supplier's internal contact names or our internal escalation system reference numbers — this will be shared in a joint review meeting with the supplier present. Where rejection rates have improved, state the number plainly without attributing the improvement to a specific cause unless that cause is confirmed in the data provided."*

The audience constraint here (the supplier will be in the room) is doing real work — without it, the model has no way to know that internal references need to be scrubbed, because nothing else in the prompt signals that this document crosses a confidentiality boundary.

### Energy & Utilities

> *"Summarise the grid load forecast deviation for the public-facing sustainability report. Do not include specific regional substation names or load figures broken out below the state level — this is for external publication. Avoid technical grid-operations terminology; assume the reader has no utilities background. If reserve margin came close to a threshold at any point, state that factually without implying it was a near-miss unless the data confirms an actual breach."*

This example stacks three different kinds of constraint at once — scope (no substation-level detail), audience (no jargon), and precision (don't imply more severity than the data supports) — which is realistic: external-facing utility content usually needs all three simultaneously, not just one.

## When this pattern fails

- **Constraints stacked so densely they fight each other.** Telling the model to be "fully comprehensive" and "extremely brief" in the same prompt forces a tradeoff the model has to silently resolve — be deliberate about which constraint wins when two pull in different directions, rather than asserting both.
- **Negative-only constraints with no positive guidance.** "Don't use jargon" tells the model what to avoid but not what to do instead — pairing it with a positive instruction ("write as if explaining to a colleague outside this department") usually produces a more reliable result than the negative instruction alone.
- **Assuming a constraint stated once will hold across a long output.** In longer generations, constraints near the start of a prompt can lose weight by the end — for long or multi-section outputs, it can help to restate the key constraint near the relevant section rather than relying on it from the top of the prompt alone.
- **Confidentiality constraints used as the only safeguard.** Telling the model not to include certain information is a strong signal, but for genuinely sensitive material, review the output rather than treating the constraint as a guarantee — it reduces the risk substantially, it doesn't eliminate the need to check.

## Combine with

Constraint setting pairs especially well with [**Role prompting**](./01-role-prompting.md) — the role sets *who* is speaking, and the constraints sharpen *how* that persona communicates and what stays in or out of scope. Together they get a draft most of the way to final without needing examples or explicit step-by-step reasoning at all.

## Quick template

```
[Your role, context, and task as normal]

CONSTRAINTS:
- Do not [specific thing to avoid].
- If [a gap or ambiguity is likely], flag it explicitly rather than assuming.
- Tone/audience: [who will read this, and what register that requires].
- Scope: [anything that must stay out of the output — internal names, figures, system references].
```

---

[← Previous: Structured output](./04-structured-output.md) &nbsp;|&nbsp; [Back to Prompting Guide](../prompting-guide.md)
