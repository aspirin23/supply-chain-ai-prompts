# AI Prompts for the Enterprise

A practitioner's guide to prompting LLMs for industry and enterprise — covering key use cases from **CPG & Retail**, **Manufacturing**, and **Energy & Utilities** industries.

This repo is built around a core prompting framework first. The industry prompt libraries are worked examples of that framework applied to real operational problems.

---

## Who this is for

- Industry professionals exploring practical LLM use cases
- Enterprise teams evaluating AI adoption in CPG, retail, manufacturing, or energy
- Industry planners and analysts looking to augment their workflow with AI
- Prompt engineers building domain-specific AI tools

## How to use this repo

1. **Read the prompting guide first** — [`prompting-guide.md`](./prompting-guide.md) gives you the framework. Even if you only want the prompts, skimming the guide will make you significantly better at adapting them.
2. **Go deeper on a pattern** — if one of the five patterns feels relevant to a problem you're working on, the [`prompt-patterns/`](./prompt-patterns/) folder has a full breakdown with industry-specific examples and failure modes.
3. **Browse the industry folders** — across the three industries (CPG/Retail, Manufacturing, Energy/Utilities) and the cross-functional general supply chain library, every prompt is a worked example of the framework applied to a specific operational problem.
4. **Copy, adapt, use** — prompts include placeholders in `[brackets]`. Swap in your own context and run them in your preferred LLM.

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

## Structure

```
enterprise-ai-prompts/
│
├── prompting-guide.md             # Start here — the core framework
│
├── prompt-patterns/
│   ├── 01-role-prompting.md       # Assigning the model a professional identity
│   ├── 02-few-shot-examples.md    # Showing the output you want, not just describing it
│   ├── 03-chain-of-thought.md     # Step-by-step reasoning for multi-step judgment calls
│   ├── 04-structured-output.md    # Specifying format, structure, and length explicitly
│   └── 05-constraint-setting.md   # Telling the model what to avoid and what not to assume
│
├── cpg-retail/
│   └── prompts.md                 # Demand forecasting, promo planning, inventory, consumer insights
│
├── manufacturing/
│   └── prompts.md                 # Production planning, supplier risk, quality, maintenance
│
├── energy-utilities/
│   └── prompts.md                 # Load forecasting, asset performance, ESG reporting, procurement
│
└── general-supply-chain/
    └── prompts.md                 # Cross-industry prompts for planning, reporting, and analysis
```

---

## Status

| File | Status |
|------|--------|
| `prompting-guide.md` | ✅ Done |
| `patterns/01-role-prompting.md` | ✅ Done |
| `patterns/02-few-shot-examples.md` | ✅ Done |
| `patterns/03-chain-of-thought.md` | ✅ Done |
| `patterns/04-structured-output.md` | ✅ Done |
| `patterns/05-constraint-setting.md` | ✅ Done |
| `cpg-retail/prompts.md` | 🔜 Coming soon |
| `manufacturing/prompts.md` | 🔜 Coming soon |
| `energy-utilities/prompts.md` | 🔜 Coming soon |
| `general-supply-chain/prompts.md` | 🔜 Coming soon |

---

## About

Built by [Anindya](https://www.linkedin.com/in/anindya-chakraborty-iimb/) — senior supply chain and AI professional, Claude Certified Architect. This repo is itself a product of applied LLM usage — researched, written, and iterated using Claude, Gemini, and GPT-4.

*Content added regularly. Star the repo to follow along.*
