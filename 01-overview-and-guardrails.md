# Localized Small Supply Chain: AI Prompts and Workflows

> **Purpose:** practical, copy-and-paste AI prompts and short step-by-step workflows that help small local businesses keep the right stuff on the shelf, line up backup suppliers, and get ready for the day a delivery doesn't show up. AI drafts, sorts and flags. The owner decides.

**In one line:** a free AI chat tool plus a simple spreadsheet can do a lot of the paperwork side of a small supply chain. It cannot see your shelves, your suppliers or your customers. You can.

> **About this guide:** an independent, self-directed portfolio project by Rashon Alsberry, written from a learner's point of view. It is not client or employer work. Every business, supplier, item and number in the examples is **fictional** and made up to show the method. Nothing here is legal, tax, food-safety, medical or financial advice.

## Who it's for

| Business | Typical supply headaches |
|---|---|
| Cafe or restaurant | Perishables, daily deliveries, running out of a menu item mid-shift |
| Winery or tasting room | Bottles, labels and corks with long waits, busy seasons |
| Small retailer | Too much of slow items, too little of the hits |
| Farm stand or market vendor | Weather, short shelf life, packaging supplies |
| Home-based maker or print-on-demand shop | Blank products and materials from one online seller |
| Small contractor | Materials that jump in price or arrive late and hold up a job |
| Local clinic (supplies only) | Gloves, paper goods and other basics that can't run out |

## Key words, in plain language

| Word | What it means here |
|---|---|
| **Supply chain** | Everyone and everything between "we need it" and "it's on the shelf": suppliers, deliveries, storage, and you. |
| **LLM** | "Large language model": the engine behind AI chat tools like ChatGPT, Claude or Gemini. |
| **Prompt** | The message you type into the AI tool. |
| **Par level** | How much of an item you want on hand right after a delivery, enough to last until the next one, plus a small cushion. |
| **Reorder point** | The "time to order" line: when stock drops to this amount, place the order. |
| **Lead time** | Days from placing an order to having it in your hands. |
| **Buffer stock** | A little extra kept on hand for the days a delivery runs late. |
| **Overstock** | More of an item than you'll use before your next order, or before it goes bad or out of style. |
| **Dead stock** | Items that haven't sold or been used in a set period you choose (for example, 90 days). |
| **Master data** | The basic records everything else depends on: item names, units, prices and supplier names. For example, the POS (point-of-sale, the register system) at a small winery keeps the menu items and their prices. |
| **Single point of failure** | One supplier, item or person that, if lost, stops a part of the business. |

## Works with any LLM

Every prompt in this guide is **model-agnostic**: it works the same way in ChatGPT, Claude, Gemini, Meta AI (Llama models), Mistral's chat assistant, Microsoft Copilot or a similar tool. Pick whichever free tool you already have; they are interchangeable here.

- **Plain text only.** Each prompt uses four labeled sections: **ROLE, CONTEXT, TASK, FORMAT** (plus **DATA** and **RULES** where needed). No special tags, no hidden "system prompt" tricks.
- **No add-ons.** No custom GPTs, Projects, Gems, Artifacts, plugins or tool calls. A plain chat window is enough.
- **Paste data inline.** Copy rows from your spreadsheet and paste them as plain text or CSV (comma-separated values: one row per line, commas between columns). See [use case 12](04-forecasting-overstock-and-dead-stock.md) for how.
- **Optional extras.** File upload or web browsing can save time if your tool has them, but nothing here depends on them.
- **Different tools give different answers.** That's normal. The "check the output" step is the same no matter which tool you use.

## The pattern behind every use case

| Step | Who | What good looks like |
|---|---|---|
| **1. Gather** | Owner | Item-level numbers and supplier names only. No customer or payment data. |
| **2. Ask** | AI tool | Copy the prompt, fill the [placeholders], paste the data. |
| **3. Check** | Owner | Re-add the key numbers. Compare with the shelf, the invoices and what you know. |
| **4. Decide** | Owner | You place the order, call the supplier, or change the plan. The AI never does. |

**Rule of thumb:** if someone asked "how do you know?", point to a count, an invoice or a sales report, never to "the AI said so."

## The nineteen use cases

| # | Use case | Page |
|---|---|---|
| 1 | Build a local supplier list | [Sourcing and suppliers](02-sourcing-and-suppliers.md) |
| 2 | Line up backup suppliers | [Sourcing and suppliers](02-sourcing-and-suppliers.md) |
| 3 | Simple supplier scorecard | [Sourcing and suppliers](02-sourcing-and-suppliers.md) |
| 4 | Compare quotes fairly | [Sourcing and suppliers](02-sourcing-and-suppliers.md) |
| 5 | Set par levels | [Inventory and ordering](03-inventory-and-ordering.md) |
| 6 | Reorder points in plain words | [Inventory and ordering](03-inventory-and-ordering.md) |
| 7 | Track spoilage and waste | [Inventory and ordering](03-inventory-and-ordering.md) |
| 8 | Turn POS sales data into an order list | [Inventory and ordering](03-inventory-and-ordering.md) |
| 9 | Forecast demand in plain words (seasons and simple averages) | [Forecasting, overstock and dead stock](04-forecasting-overstock-and-dead-stock.md) |
| 10 | Spot and fix overstock | [Forecasting, overstock and dead stock](04-forecasting-overstock-and-dead-stock.md) |
| 11 | Find and clear dead stock | [Forecasting, overstock and dead stock](04-forecasting-overstock-and-dead-stock.md) |
| 12 | Paste a spreadsheet to find stocking patterns (sample CSV) | [Forecasting, overstock and dead stock](04-forecasting-overstock-and-dead-stock.md) |
| 13 | Track lead times with a simple log | [Supplier lead times for local vendors](05-supplier-lead-times.md) |
| 14 | Compare local vendors on reliability and variability | [Supplier lead times for local vendors](05-supplier-lead-times.md) |
| 15 | Plan around lead times (reorder timing, buffer, backups, holidays; sample CSV) | [Supplier lead times for local vendors](05-supplier-lead-times.md) |
| 16 | Check for single-supplier dependence | [Risk, disruption and records](06-risk-disruption-and-records.md) |
| 17 | Write a one-page disruption playbook | [Risk, disruption and records](06-risk-disruption-and-records.md) |
| 18 | Clean up master data (duplicate items and vendors) | [Risk, disruption and records](06-risk-disruption-and-records.md) |
| 19 | Draw a simple local supply map | [Risk, disruption and records](06-risk-disruption-and-records.md) |

Every use case has the same parts: **the problem** in one line, a **ready-to-copy prompt** with [placeholders], a **workflow** of 3-6 steps, a **worked example** (fictional), and a **check the output** line naming what the AI can't know.

## Worked examples, start to finish
Three fictional scenarios put the prompts together with sample data. Paste the CSV text into any AI chat tool, or upload the file if your tool allows it.

| Scenario | Sample data | Prompts used |
|---|---|---|
| [A small cafe's weekly stock: waste and par levels](use-cases/cafe-weekly-stock.md) | Stock sheet | 12, 7, 5 |
| [A local retailer's forecast, overstock and dead stock](use-cases/retail-forecast-overstock-dead-stock.md) | Sales history | 9, 10, 11 |
| [A buyer comparing local vendors' lead times and reliability](use-cases/vendor-lead-times-reliability.md) | Delivery log | 14, 15 |

## Guardrails

| Risk | What goes wrong | Guardrail |
|---|---|---|
| **Private data** | Customer names, card numbers or staff details pasted into a chat tool leave your control. | Paste item-level numbers only. Delete customer, payment and staff columns first. |
| **Wrong math** | AI tools can add up columns wrong or skip rows, and still sound sure. | Re-add the key totals yourself, in the spreadsheet. |
| **Made-up facts** | The AI may invent supplier names, prices, rules or "industry averages." | Use only suppliers and prices you found yourself. Ignore any number the AI didn't get from your data. |
| **Missing context** | The AI doesn't know about the street fair next week or the supplier who's retiring. | Add what you know to the CONTEXT section. Trust your local knowledge over the AI. |
| **Rules and safety** | Food safety, alcohol, medical-supply and tax rules vary by place. | Check those with the official source or a professional, never with an AI answer. |
| **Over-trust** | A neat table looks finished, so nobody checks it. | Treat every AI answer as a first draft from a new helper. |

**Hard "no" list:**
- [ ] No customer names, emails, phone numbers or addresses in a prompt
- [ ] No card numbers, bank details or payment records
- [ ] No staff personal details or patient information
- [ ] No order placed, supplier dropped or price changed just because the AI suggested it
- [ ] No number used until you've checked it against your own records

**Before you paste, check:**
- [ ] Only the columns the prompt needs (item, unit, counts, dates, supplier)
- [ ] Supplier contact details removed if you don't need them for the task
- [ ] Your AI tool's privacy or data settings reviewed (many let you turn off use of your chats for training)

## Free tools that work for this

All of these are examples, not recommendations. Use what you already have. Free plans and limits change often.

| Need | Free options (interchangeable) |
|---|---|
| AI chat | ChatGPT, Claude, Gemini, Meta AI, Mistral's chat assistant, Microsoft Copilot (free plans) |
| Spreadsheet | Google Sheets, LibreOffice Calc, or the spreadsheet you already use |
| Inventory system (optional, bigger step) | Odoo Community edition, a free, open-source business app with an Inventory module ([LGPLv3 license](https://github.com/odoo/odoo/blob/master/LICENSE); Inventory module manifest: [addons/stock](https://github.com/odoo/odoo/blob/master/addons/stock/__manifest__.py)) |
| Your own POS | Most POS systems can export sales by item as a CSV file |

## Try it this week

- [ ] Pick your 10 most important items. Put them in a sheet with item, unit, supplier, and weekly use.
- [ ] Run the supplier-dependence prompt ([use case 16](06-risk-disruption-and-records.md)) on that list.
- [ ] For your top "high" item, run the backup-supplier workflow ([use case 2](02-sourcing-and-suppliers.md)).
- [ ] Start a lead-time log ([use case 13](05-supplier-lead-times.md)) for your two most important vendors.
- [ ] Export one month of item sales from your POS and try [use case 12](04-forecasting-overstock-and-dead-stock.md).
- [ ] Write down one thing the AI got wrong. That's the most useful part.

Next: [Sourcing and suppliers](02-sourcing-and-suppliers.md) · Sources: [sources and claims to verify](sources.md)

---

Back to [README](README.md)

Rashon Alsberry, independent portfolio project - [starboy1968.github.io](https://starboy1968.github.io)
