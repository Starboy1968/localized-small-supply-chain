# Localized Small Supply Chain: AI Prompts and Workflows

**Copy-and-paste AI prompts and short workflows for small local businesses: suppliers, inventory, forecasting, overstock and dead stock, vendor lead times, and supply risk.**

For cafes and restaurants, wineries, small retailers, farm stands and market vendors, home-based makers and print-on-demand shops, small contractors, and local clinics' supplies.

> An independent portfolio project: self-directed, not client or employer work. Every business, supplier and number in the examples is fictional. Not legal, tax, food-safety, medical or financial advice.

## Contents
- [What it is](#what-it-is)
- [Works with any LLM](#works-with-any-llm)
- [The 19 use cases](#the-19-use-cases)
- [Guardrails](#guardrails)
- [Repo map](#repo-map)
- [Related projects](#related-projects)

## What it is
Nineteen plain-language use cases. Each one has the problem in one line, a ready-to-copy prompt with [placeholders], a 3-6 step workflow, a fictional worked example, and a "check the output" line. Math stays at add, subtract, multiply; risk is rated LOW / MEDIUM / HIGH. Free tools only.

## Works with any LLM
Every prompt is plain text with labeled **ROLE / CONTEXT / TASK / FORMAT** sections, and data is pasted inline as plain text or CSV. No vendor-specific tags, custom GPTs, Projects, Gems, Artifacts, plugins or tool calls. They work the same in ChatGPT, Claude, Gemini, Meta AI (Llama), Mistral's assistant, Copilot or similar tools. File upload and browsing are optional extras.

## The 19 use cases

| # | Use cases | Page |
|---|---|---|
| 1-4 | Local supplier list, backup suppliers, supplier scorecard, quote comparison | [02 Sourcing and suppliers](02-sourcing-and-suppliers.md) |
| 5-8 | Par levels, reorder points, spoilage and waste, POS data to an order list | [03 Inventory and ordering](03-inventory-and-ordering.md) |
| 9-12 | Forecasting in plain words, overstock, dead stock, pasting a spreadsheet to find patterns (sample CSV) | [04 Forecasting, overstock and dead stock](04-forecasting-overstock-and-dead-stock.md) |
| 13-15 | Lead-time log, comparing vendor reliability and variability, planning around lead times (sample CSV) | [05 Supplier lead times for local vendors](05-supplier-lead-times.md) |
| 16-19 | Single-supplier dependence, disruption playbook, clean master data, local supply map | [06 Risk, disruption and records](06-risk-disruption-and-records.md) |

## Guardrails
AI drafts, humans decide. No customer, payment, staff or patient data in a prompt. Re-check every number in your own sheet. Rules on food safety, alcohol, medical supplies and tax come from official sources, not the AI. Full list: [01 Overview and guardrails](01-overview-and-guardrails.md#guardrails).

## Repo map

| File | What's inside |
|---|---|
| [01-overview-and-guardrails.md](01-overview-and-guardrails.md) | Who it's for, key words, works with any LLM, all use cases, guardrails, free tools |
| [02-sourcing-and-suppliers.md](02-sourcing-and-suppliers.md) | Use cases 1-4 |
| [03-inventory-and-ordering.md](03-inventory-and-ordering.md) | Use cases 5-8 |
| [04-forecasting-overstock-and-dead-stock.md](04-forecasting-overstock-and-dead-stock.md) | Use cases 9-12 |
| [05-supplier-lead-times.md](05-supplier-lead-times.md) | Use cases 13-15 |
| [06-risk-disruption-and-records.md](06-risk-disruption-and-records.md) | Use cases 16-19 |
| [sample-data/](sample-data/) | Fictional CSVs: [cafe weekly stock](sample-data/cafe-weekly-stock.csv), [vendor lead-time log](sample-data/vendor-lead-time-log.csv) |
| [sources.md](sources.md) | Checked sources and claims to verify |

## Related projects
- [AI for CISA and IT Auditors](https://github.com/Starboy1968/ai-for-it-auditors): nine practical ways AI can speed up IT audit work, with a human check at every step.
- [AI Supply Chain Risk Assessment](https://github.com/Starboy1968/ai-supply-chain-risk-assessment): nine scored AI-related supply chain risks, with controls, KRIs and a 30/60/90-day plan.
- [AI-Assisted Risk Analysis](https://github.com/Starboy1968/ai-assisted-risk-analysis): a reusable risk-analysis prompt and a worked example where a human corrects the AI draft.
- [Reading the Room: Power and Behavior Risk Indicators](https://github.com/Starboy1968/power-behavior-risk-indicators): observable signs of how power and incentives shape risk decisions.
- [Behavioral Supply Chain Risk: Human Factors, AI, and Audit](https://github.com/Starboy1968/behavioral-supply-chain-risk-audit-ai): how bias and pressure create supply chain risk, and how review helps catch it.
- [Playing the Risk Game](https://github.com/Starboy1968/supply-chain-ai-governance-strategy): plain-language game theory for supply chain risk and AI governance.
- [AI in Supply Chain Operations](https://github.com/Starboy1968/ai-in-supply-chain-operations): how a supply chain manager can use AI in six everyday jobs.
- [Healthcare Cyber Risk Program: An OSINT Case Study](https://github.com/Starboy1968/healthcare-cyber-risk-osint-case-study): a cyber risk program for a fictional health system, from public sources.
- [Two Suppliers, One Factory](https://github.com/Starboy1968/two-suppliers-one-factory): finding hidden tier-2 single points of failure.
- [ICM Assistant Workspace](https://github.com/Starboy1968/icm-assistant-workspace): a model-agnostic, five-layer folder workspace that guides any AI chat model through intake, research, drafting and review, with rules for copyright, wellbeing and fairness.
- Portfolio site: [starboy1968.github.io](https://starboy1968.github.io)

## Author
Rashon Alsberry, independent portfolio project - [starboy1968.github.io](https://starboy1968.github.io)
