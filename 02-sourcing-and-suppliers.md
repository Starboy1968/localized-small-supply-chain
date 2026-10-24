# Sourcing and Suppliers

Part of [Localized Small Supply Chain: AI Prompts and Workflows](01-overview-and-guardrails.md). Use cases 1-4.

All examples are **fictional**. Supplier names are letters (Supplier A, B, C) on purpose. Every prompt is plain text and works in any AI chat tool.

---

## 1. Build a local supplier list

**The problem:** your suppliers live in your head, a phone, and a pile of invoices, so nobody else can reorder when you're out.

**Prompt (copy, fill the [brackets], paste your data)**
```
ROLE: You are a careful office helper for a small [type of business] in [town or region].
CONTEXT: I want one clean list of every supplier I buy from. My notes are messy.
DATA (plain text, pasted from invoices or notes):
[paste item names, supplier names, what you buy from each, how you order]
TASK: Turn my notes into a supplier list. One row per supplier.
FORMAT: A table with columns: Supplier | What I buy | How I order (phone, website, rep visit, market) | Usual delivery day | Notes.
RULES: Use only the suppliers in my data. Do not add or suggest suppliers. If something is unclear, write "ASK OWNER".
```

**Workflow**
1. Gather the last 2-3 months of invoices or receipts.
2. Type or paste supplier names and items into the prompt. Leave out account numbers and payment details.
3. Run the prompt and paste the table into your spreadsheet.
4. Fill every "ASK OWNER" cell yourself.
5. Save it where a second person can find it.

**Worked example (fictional):** a farm stand's notes say "berries from the grower down the road, clamshells online, eggs from two neighbors, honey on consignment." The AI returns a 5-row table and marks "eggs: which neighbor supplies which day? ASK OWNER." The owner fills it in from memory in two minutes.

**Check the output:** the AI only knows what you pasted. It can't tell if a supplier has closed or changed prices. Check each row against a recent invoice.

---

## 2. Line up backup suppliers

**The problem:** when your one supplier for an item is out, you start looking for a new one in a hurry, at the worst time.

**Prompt**
```
ROLE: You are a planning helper for a small [type of business].
CONTEXT: My main supplier for [item] is [Supplier A]. I need a backup before something goes wrong. I'm in [town or region] and can travel [distance].
TASK: Give me a checklist of TYPES of places that might sell [item] (for example: wholesale clubs, restaurant supply stores, other local producers, online sellers) and the questions to ask each one before I rely on it.
FORMAT: Two lists. 1) Types of places to look. 2) Questions to ask a possible backup (minimum order, lead time, quality, payment terms, delivery area).
RULES: Do not name specific businesses. I will find real ones myself.
```

**Workflow**
1. Pick your top 3 items where running out would hurt most.
2. Run the prompt for each.
3. Use the "types of places" list to find 1-2 real local options yourself (search, ask other owners, visit).
4. Ask each one the AI's questions. Write the answers down.
5. Place a small test order before you need it, so you know the backup really works.

**Worked example (fictional):** a small clinic buys exam gloves from one distributor. The AI lists types of backups: a second medical distributor, a local pharmacy's business desk, a wholesale club. The office manager calls two of them and learns one needs a business account set up in advance. They set it up now, not during a shortage.

**Check the output:** the AI can't confirm any place really stocks your item, delivers to you or meets quality rules. For clinic or food items, confirm that the backup's product meets your own requirements.

---

## 3. Simple supplier scorecard

**The problem:** you have a feeling one supplier is unreliable, but nothing written down to back it up.

**Prompt**
```
ROLE: You are a fair, practical reviewer helping a small [type of business] rate its suppliers.
CONTEXT: I rate suppliers as LOW, MEDIUM or HIGH concern. No numbers or formulas.
DATA (plain text or CSV):
[paste: supplier, on-time notes, quality notes, communication notes, price changes in the last few months]
TASK: For each supplier, give a LOW / MEDIUM / HIGH concern rating for: on time, quality, communication, price stability. Then an overall rating.
FORMAT: A table: Supplier | On time | Quality | Communication | Price stability | Overall | One-line reason.
RULES: Base every rating only on my notes. If my notes don't cover something, write "NO DATA", not a guess. Explain each HIGH in one plain sentence.
```

**Workflow**
1. Keep a simple running note for each supplier: late or on time, any bad product, how fast they reply.
2. Once a month, paste the notes into the prompt.
3. Read each HIGH. Do you agree? Change any rating you disagree with.
4. Talk to any supplier with a HIGH before you think about switching.

**Worked example (fictional):**

| Supplier | On time | Quality | Communication | Price stability | Overall | Reason |
|---|---|---|---|---|---|---|
| Supplier A (produce) | LOW | MEDIUM | LOW | MEDIUM | LOW | One bruised case in 3 months, otherwise steady |
| Supplier B (dry goods) | HIGH | LOW | MEDIUM | LOW | MEDIUM | Late 3 of the last 6 deliveries |
| Supplier C (paper goods) | LOW | LOW | NO DATA | HIGH | MEDIUM | Price went up twice; no notes on replies |

**Check the output:** the ratings are only as fair as your notes. One bad week can look like a pattern. The AI doesn't know about any side of the story you didn't write down.

---

## 4. Compare quotes fairly

**The problem:** the lowest price per unit isn't always the lowest real cost once delivery fees, minimums and wait times are added.

**Prompt**
```
ROLE: You are a careful purchasing helper for a small [type of business].
CONTEXT: I need [quantity] of [item] by [date]. I have quotes from several suppliers.
DATA (plain text):
[paste each quote: supplier, price per unit, delivery fee, minimum order, days to deliver, other terms]
TASK: Work out the total cost for MY quantity from each supplier, including delivery and any minimum order. Say which ones can deliver by my date.
FORMAT: A table: Supplier | Price per unit | Units I'd have to buy | Delivery fee | Total cost | Arrives by my date? | Notes. Show the simple math for each total in one line.
RULES: Use only the numbers I gave you. Don't pick a winner. List the trade-offs.
```

**Workflow**
1. Get quotes in writing (email or text) so the numbers are clear.
2. Paste them into the prompt.
3. Re-do each total yourself with a calculator.
4. Weigh the trade-offs (price vs. speed vs. reliability) and decide.

**Worked example (fictional):** a small clinic needs 50 boxes of gloves within a week.

| Supplier | Price per box | Must buy | Delivery fee | Total | On time? |
|---|---|---|---|---|---|
| Supplier A | $8.00 | 50 | $0 | 50 × $8.00 = **$400** | Yes (5 days) |
| Supplier B | $7.50 | 50 | $40 | 50 × $7.50 + $40 = **$415** | Yes (2 days) |
| Supplier C | $7.20 | 100 (minimum) | $0 | 100 × $7.20 = **$720** | Yes (4 days) |

Supplier C has the lowest unit price but the highest total, because of its minimum. Supplier A is cheapest for this order; B costs $15 more but arrives 3 days sooner. The office manager decides.

**Check the output:** AI tools can multiply wrong. Re-do every total. The AI also can't tell you if a quote is still valid or if the products are truly the same.

---

Next: [Inventory and ordering](03-inventory-and-ordering.md) · Back to [overview](01-overview-and-guardrails.md)

---

Back to [README](README.md)

Rashon Alsberry, independent portfolio project - [starboy1968.github.io](https://starboy1968.github.io)
