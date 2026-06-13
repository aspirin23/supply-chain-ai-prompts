# Supply Chain AI Prompts

A practitioner's guide to prompting LLMs for supply chain, operations, and industry work — covering **CPG & Retail**, **Manufacturing**, and **Energy & Utilities**.

This repo is built around a core prompting framework first. The industry prompt libraries are worked examples of that framework applied to real operational problems — not a generic collection of copy-paste snippets.

---

## What's inside

**[prompting-guide.md](./prompting-guide.md)** — Start here. A structured guide to writing effective prompts for supply chain and operations contexts: how to frame business problems for LLMs, how to provide the right context, and how to get outputs that are actually useful in professional settings.

**Industry prompt libraries** — Worked examples of the framework applied to four domains, each prompt tied to a specific operational scenario.

---

## Who this is for

- Supply chain planners and analysts looking to augment their workflow with AI
- Operations professionals exploring practical LLM use cases
- Enterprise teams evaluating AI adoption in CPG, retail, manufacturing, or energy
- Prompt engineers building domain-specific AI tools

---

## Structure

```
supply-chain-ai-prompts/
│
├── prompting-guide.md            # Start here — the core framework
│
├── cpg-retail/
│   └── prompts.md                # Demand forecasting, promo planning, inventory, consumer insights
│
├── manufacturing/
│   └── prompts.md                # Production planning, supplier risk, quality, maintenance
│
├── energy-utilities/
│   └── prompts.md                # Load forecasting, asset performance, ESG reporting, procurement
│
└── general-supply-chain/
    └── prompts.md                # Cross-industry prompts for planning, reporting, and analysis
```

---

## How to use this repo

1. **Read the prompting guide first** — [`prompting-guide.md`](./prompting-guide.md) gives you the framework. Even if you only want the prompts, skimming the guide will make you significantly better at adapting them.
2. **Browse the industry folders** — each prompt is a worked example of the framework applied to a specific operational problem.
3. **Copy, adapt, use** — prompts include placeholders in `[brackets]`. Swap in your own context and run them in [Claude](https://claude.ai) or your preferred LLM.

---

## Industries covered

| Industry | Focus areas |
|----------|-------------|
| 🛒 CPG & Retail | Demand forecasting, promotion planning, inventory optimisation, consumer behaviour, last-mile logistics |
| 🏭 Manufacturing | Production planning, capacity optimisation, supplier risk, predictive maintenance, quality control |
| ⚡ Energy & Utilities | Load forecasting, asset performance, grid optimisation, ESG reporting, energy procurement |
| 📦 General Supply Chain | S&OP, risk summarisation, KPI analysis, stakeholder reporting, scenario planning |

---

## Prompt format

Every prompt in the industry libraries follows this structure:

```
### Prompt name
**Use case:** What business problem this solves
**When to use:** The scenario or trigger for using this prompt
**Prompt:** The actual prompt text — ready to copy and adapt
**Why this works:** How this prompt applies the framework principles
```

The **Why this works** section is what separates this from a plain prompt dump — it explains the prompting logic so you can adapt and extend each example yourself.

---

## Status

| File | Status |
|------|--------|
| `prompting-guide.md` | 🔜 Coming soon |
| `cpg-retail/prompts.md` | 🔜 Coming soon |
| `manufacturing/prompts.md` | 🔜 Coming soon |
| `energy-utilities/prompts.md` | 🔜 Coming soon |
| `general-supply-chain/prompts.md` | 🔜 Coming soon |

---

## About

Built by [Anindya](https://www.linkedin.com/in/anindya-chakraborty-iimb/) — senior supply chain and AI professional, Claude Certified Architect. Connect on LinkedIn for posts on enterprise AI, supply chain, and practical LLM applications.

*Content added regularly. Star the repo to follow along.*