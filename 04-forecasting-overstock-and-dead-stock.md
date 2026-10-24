# Forecasting, Overstock and Dead Stock

Part of [Localized Small Supply Chain: AI Prompts and Workflows](01-overview-and-guardrails.md). Use cases 9-12.

All examples are **fictional**. No heavy math: averages, "about 1.5 times," and add/subtract only. Every prompt is plain text and works in any AI chat tool. Data is pasted inline as plain text or CSV; file upload is an optional extra.

---

## 9. Forecast demand in plain words

**The problem:** you guess how much you'll need next month, and the guess is often off in busy or slow seasons.

**Forecast, in plain words:** a careful guess about how much you'll sell or use soon, based on what happened before. Two simple tools:
- **Simple average:** add up the last few weeks and divide by the number of weeks.
- **Seasonal pattern:** something that rises or falls at about the same time each year (holidays, harvest, tourist season, school calendar).

**Prompt**
```
ROLE: You are a planning helper for a small [type of business]. Keep everything in plain words and simple arithmetic.
CONTEXT: I want a starting guess for how much [item or items] I'll need in [coming period]. Things I know are coming: [events, holidays, weather, closures, or "none"].
DATA (CSV: period, item, units sold or used). Include the same period last year if I have it:
[paste rows]
TASK: 1) Give the simple average of the most recent [number] periods. 2) If last year's data is there, say whether the coming period was higher or lower than the periods before it, and by about how much (for example, "about 1.5 times"). 3) Combine those into one starting guess, with a low and a high.
FORMAT: A short table: Item | Recent average | Seasonal note | Starting guess (low / likely / high). Then 2-3 lines explaining your reasoning in plain words.
RULES: Show your math. Use only my numbers and the events I listed. Say clearly when there's too little data to see a pattern.
```

**Workflow**
1. Pull weekly or monthly totals for your key items (POS export or your counts).
2. If you have last year's numbers for the same season, include them.
3. Add anything you know is coming to the CONTEXT line.
4. Run the prompt and re-do the average yourself.
5. Use the "likely" number to set pars ([use case 5](03-inventory-and-ordering.md)); keep the "high" number in mind for backup orders.
6. After the period ends, compare the guess with what really happened, and note it.

**Worked example (fictional):**
- *Simple average:* a farm stand sold 40, 44, 38 and 42 baskets of tomatoes in the last four weeks. 40 + 44 + 38 + 42 = 164. 164 ÷ 4 = **41 a week**.
- *Seasonal pattern:* a winery's tasting room sold about 40 bottles a week of its red blend last September and about 60 a week last October, about **1.5 times** as many. This September is averaging 44 a week, so a starting guess for October is about 44 × 1.5 = **66 a week** (low 55, high 70, chosen by the owner).

**Check the output:** with only a few weeks of data, a "pattern" may just be chance. The AI doesn't know about new competitors, road work or a weather event unless you tell it. The forecast is a starting point; you set the order.

---

## 10. Spot and fix overstock

**The problem:** cash and shelf space are stuck in items you'll take months to sell or use.

**Overstock, in plain words:** more of an item than you'll use before your next order or before it goes bad, out of date or out of style.

**Weeks of cover (simple check):** on hand ÷ weekly use = how many weeks it will last.

**Prompt**
```
ROLE: You are an inventory helper for a small [type of business].
CONTEXT: I want to know which items I have too much of. My target is about [number] weeks of stock for most items. Items that expire or go out of season: [list or "none"].
DATA (CSV: item, unit, on hand, average use or sales per week, cost per unit, expiry or season end if any):
[paste rows]
TASK: For each item, work out weeks of cover (on hand divided by weekly use). List items above my target, and how many units are extra. For each, suggest options from this list only: pause or shrink the next reorder, bundle with a faster seller, mark down, return to supplier if allowed, move to another sales channel (market stall, online), use in another product.
FORMAT: Table: Item | On hand | Weekly use | Weeks of cover | Extra units | Suggested options. Show the math.
RULES: Use only my numbers. Don't promise any option will work. Put items close to expiry or season end at the top.
```

**Workflow**
1. Count or export on-hand amounts and average weekly use.
2. Run the prompt.
3. Re-do the weeks of cover for the top 3 items.
4. Pick one action per item. The easiest first step is often **pausing the next reorder**.
5. Lower the par level ([use case 5](03-inventory-and-ordering.md)) so it doesn't build up again.

**Worked example (fictional):** a small retailer has 120 candles on hand and sells about 10 a week. 120 ÷ 10 = **12 weeks of cover**. The target is 4 weeks (40 candles), so about 120 − 40 = **80 are extra**. Options: skip the next two reorders, bundle a candle with a mug for a gift set, and mark down one scent that sells slowest.

**Check the output:** the AI doesn't know your margins, supplier return rules or how customers will react to a markdown. Check any return terms with the supplier directly.

---

## 11. Find and clear dead stock

**The problem:** some items haven't moved in months, and they quietly cost you money every week they sit there.

**Dead stock, in plain words:** items that haven't sold or been used in a period you choose (for example, 90 days). Pick a period that fits your business: shorter for food, longer for hardware.

**The cost of holding it (in words, not formulas):**
- Cash tied up: units × what you paid
- Shelf or storage space you could use for items that sell
- Risk of going bad, expiring, fading or going out of style
- Time spent counting, moving and cleaning around it
- Any storage fees you pay

**Prompt**
```
ROLE: You are an inventory helper for a small [type of business].
CONTEXT: I call an item "dead stock" if it hasn't sold or been used in [number] days.
DATA (CSV: item, units on hand, cost per unit, last sale or use date, today's date):
[paste rows]
TASK: 1) List items that meet my dead-stock rule, oldest first. 2) For each, show cash tied up (units times cost). 3) List holding costs in plain words (space, spoilage, time). 4) Suggest options to clear it: bundle, discount, sell at a market or online, return or trade with supplier, repurpose or use in-house, donate.
FORMAT: Table: Item | Days since last sale | Units | Cash tied up | Suggested options. Then a short "what to stop doing" note.
RULES: Use only my data. Show the math. Do not give tax or legal advice about donations or write-offs; say "check with a tax professional" if that comes up.
```

**Workflow**
1. Export or list each item's last sale or use date.
2. Choose your dead-stock period.
3. Run the prompt and re-check the "cash tied up" for the biggest items.
4. Pick one clearing option per item and set a date to decide if it worked.
5. Stop reordering that item, or order it only on request.

**Worked example (fictional):** a home-based maker has 40 tote bags in an old design that cost $6 each. None have sold in 4 months. Cash tied up: 40 × $6 = **$240**, plus a shelf of space. Options: bundle a tote free with orders over a set amount, sell them at the next craft market, or reuse the blanks with a new design if the print can be covered.

**Check the output:** the AI can't tell if an item is seasonal and about to sell again (holiday or harvest items). It also can't advise on taxes for donations or write-offs.

---

## 12. Paste a spreadsheet to find stocking patterns

**The problem:** your counts are in a spreadsheet, but you don't have time to stare at it and spot what's going wrong.

### Columns to include

| Column | Why it matters |
|---|---|
| week (or date) | Shows change over time |
| item | What it is (use one consistent name) |
| unit | Case, bag, bottle, carton |
| start | On hand at the start of the period |
| received | Delivered during the period |
| used_or_sold | Used or sold during the period |
| wasted | Thrown out (expired, damaged) |
| end | On hand at the end |
| ran_out | yes / no: did you run out at any point? |
| supplier | Supplier name or letter (no contact details) |

Optional: cost per unit, expiry date, notes (events, weather). Leave out anything not needed.

### Privacy check before pasting
- [ ] No customer names, emails, phone numbers or addresses
- [ ] No card, bank or payment columns
- [ ] No staff names or schedules
- [ ] No patient information (clinics)
- [ ] Supplier contact details and account numbers removed
- [ ] Only the rows you need (for example, the last 4-12 weeks)

### How to paste a CSV as plain text (works in any LLM)
1. In your spreadsheet, select the header row and the data rows.
2. Copy and paste them right into the chat box. Most tools accept this as tab-separated text, which works fine.
3. Or, for clean CSV: use File > Download (or Save as) > CSV, open the file in a plain text editor (Notepad, TextEdit in plain-text mode), and copy the text.
4. Paste it under the **DATA** line of the prompt.
5. Keep it short. If the tool cuts off or loses rows, paste fewer rows or one item group at a time.
6. *Optional extra:* if your tool supports file upload, you can attach the CSV instead. The prompt stays the same.

### Prompt
```
ROLE: You are a careful inventory analyst helping a small [type of business]. Use plain words and simple arithmetic only.
CONTEXT: Below is my stock sheet for [time period]. Each row is one item for one week. Columns: week, item, unit, start, received, used_or_sold, wasted, end, ran_out, supplier. Things I know about: [events, menu changes, or "none"].
DATA (CSV):
[paste the CSV text here]
TASK:
1) Check each row: start + received - used_or_sold - wasted should equal end. List any row that doesn't add up.
2) Find stocking patterns: items that ran out, items building up (overstock), items barely moving (possible dead stock), items with steady waste.
3) For each pattern, show your reasoning: which rows and numbers you used.
4) Give each pattern a confidence level: HIGH, MEDIUM or LOW, with a one-line reason. Use LOW when there are only a few weeks, missing data, or the pattern could be seasonal.
5) Suggest one small next step per pattern.
FORMAT:
- Table A, "Rows that don't add up": Week | Item | Expected end | Recorded end.
- Table B, "Patterns": Item | Pattern | Evidence (rows and numbers) | Confidence | Suggested next step.
- A short list: "What I can't tell from this data."
RULES: Use only the data above. Do not invent rows, items or numbers. If something is unclear, say so instead of guessing.
```

### Workflow
1. Copy the columns above into your sheet (or rename yours to match).
2. Run the privacy check.
3. Paste the CSV into the prompt and run it.
4. Read Table A first. Fix data errors before trusting any pattern.
5. **Verify in the sheet itself** (next section). Don't act on a pattern you can't see in your own numbers.
6. Act on HIGH-confidence patterns; watch MEDIUM and LOW ones for a few more weeks.

### Sample CSV (fictional cafe, 3 weeks, 15 rows)
A copy is in [sample-data/cafe-weekly-stock.csv](sample-data/cafe-weekly-stock.csv).

```
week,item,unit,start,received,used_or_sold,wasted,end,ran_out,supplier
W1,Oat milk,carton,6,12,18,0,0,yes,Supplier A
W2,Oat milk,carton,0,12,12,0,0,yes,Supplier A
W3,Oat milk,carton,0,18,17,0,1,no,Supplier A
W1,Whole milk,gallon,4,20,21,1,2,no,Supplier A
W2,Whole milk,gallon,2,20,19,1,2,no,Supplier A
W3,Whole milk,gallon,2,20,20,0,2,no,Supplier A
W1,Muffin mix,bag,10,6,5,0,11,no,Supplier B
W2,Muffin mix,bag,11,6,4,0,13,no,Supplier B
W3,Muffin mix,bag,13,6,5,1,13,no,Supplier B
W1,Pumpkin syrup,bottle,9,0,1,0,8,no,Supplier B
W2,Pumpkin syrup,bottle,8,0,0,0,8,no,Supplier B
W3,Pumpkin syrup,bottle,8,0,0,0,8,no,Supplier B
W1,Paper cups 12oz,sleeve,10,0,6,0,4,no,Supplier C
W2,Paper cups 12oz,sleeve,4,10,6,0,8,no,Supplier C
W3,Paper cups 12oz,sleeve,8,0,6,0,3,no,Supplier C
```

### Worked example: what a good answer looks like (fictional)

**Table A: rows that don't add up**

| Week | Item | Expected end | Recorded end |
|---|---|---|---|
| W3 | Paper cups 12oz | 8 + 0 − 6 − 0 = 2 | 3 |

**Table B: patterns**

| Item | Pattern | Evidence | Confidence | Next step |
|---|---|---|---|---|
| Oat milk | Running out | Ended at 0 in W1 and W2, ran_out = yes both weeks. Used 18 when 18 were there; 12 when only 12 arrived. | MEDIUM: when you run out, the real demand is hidden, so it may be even higher | Raise the weekly order from 12 to about 18 and watch |
| Muffin mix | Building up (overstock) | Receives 6 a week, uses 4-5. End went 11 → 13 → 13. | MEDIUM: only 3 weeks, but steady direction | Skip or shrink one delivery; lower the par |
| Pumpkin syrup | Barely moving (possible dead stock) | 1 used in 3 weeks; 8 still on hand | LOW: could be seasonal and about to pick up; 3 weeks is short | Check the season and the expiry date before deciding |
| Whole milk | Steady, small waste | Used 19-21 a week; wasted 1, 1, 0; ends at 2 each week | HIGH: consistent all 3 weeks | No change; keep logging waste |
| Paper cups 12oz | Data error | W3 doesn't add up (see Table A) | n/a | Recount cups before using this row |

**What I can't tell from this data:** prices, why oat milk demand changed, whether pumpkin syrup is a seasonal special, and whether the cup count error is a miscount or a missing entry.

### Verify the patterns in the sheet itself
- [ ] Add a **check** column: `=D2+E2-F2-G2-H2` (start + received − used − wasted − end). Every row should show 0. In the sample, W3 paper cups shows −1, matching Table A.
- [ ] Filter **ran_out = yes**. Do the same items show up that the AI named?
- [ ] For each "building up" item, look at the **end** column week to week. Is it really rising?
- [ ] For each "barely moving" item, look at **used_or_sold**. Is it really near zero?
- [ ] If the AI named a pattern you can't see in the sheet, drop it.

**Check the output:** AI tools can skip rows, misread columns or add wrong, especially with long pastes. The confidence levels are the AI's opinion, not a measurement. Only your sheet and your shelf are the source of truth.

---

Next: [Supplier lead times for local vendors](05-supplier-lead-times.md) · Back to [overview](01-overview-and-guardrails.md)

---

Back to [README](README.md)

Rashon Alsberry, independent portfolio project - [starboy1968.github.io](https://starboy1968.github.io)
