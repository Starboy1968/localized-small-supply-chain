# Supplier Lead Times for Local Vendors

Part of [Localized Small Supply Chain: AI Prompts and Workflows](01-overview-and-guardrails.md). Use cases 13-15.

All examples are **fictional**. Vendors are letters (Vendor A, B, C) on purpose. Math stays at "subtract two dates, count, find the longest and shortest." Every prompt is plain text and works in any AI chat tool; data is pasted inline as CSV, or uploaded as a file if your tool allows it.

**Lead time, in plain words:** the number of days from placing an order to having it in your hands. A vendor's **promised** lead time is what they say; the **actual** lead time is what happens.

**Two things to know about any vendor:**
- **Reliability:** how often they deliver on or before the promised day.
- **Variability:** how much their delivery time jumps around. A vendor who always takes 4 days is easier to plan around than one who takes 1 day some weeks and 5 days others.

**See it end to end:** [Worked example 3: comparing local vendors](use-cases/vendor-lead-times-reliability.md) (use cases 14 and 15).

---

## 13. Track lead times with a simple log

**The problem:** you feel like a vendor is "always late," but you don't have the dates to show it, or to plan around it.

### The log: columns to keep

| Column | What to write |
|---|---|
| order_id | Any number, so you can find the row |
| vendor | Vendor name or letter (no contact details needed) |
| item | What you ordered |
| order_date | The day you placed the order |
| promised_date | The day they said it would arrive |
| received_date | The day it actually arrived (in full) |

Then let the spreadsheet work out two more columns (see "Verify" below):
- **actual_days** = received date − order date
- **days_late** = received date − promised date (0 = on time, a positive number = late, a negative number = early)

**Prompt**
```
ROLE: You are a careful record-keeping helper for a small [type of business].
CONTEXT: I keep a lead-time log for my local vendors. Dates are in YYYY-MM-DD format.
DATA (CSV: order_id, vendor, item, order_date, promised_date, received_date):
[paste rows]
TASK: For each row, work out: promised_days (promised_date minus order_date), actual_days (received_date minus order_date), and days_late (received_date minus promised_date; negative means early).
FORMAT: The same table with those three columns added. Then one line per vendor: number of orders, number late, number early.
RULES: Use only my dates. Show one example calculation. If a date is missing or looks wrong, flag the row instead of guessing.
```

**Workflow**
1. Start the log today. Add a row every time you place an order.
2. Fill in received_date the day it arrives. If it came in short, note it (a partial delivery isn't "received").
3. Once you have 4 or more orders per vendor, paste the log into the prompt.
4. Check the AI's days against your own sheet (formulas below).
5. Keep logging. Use cases 14 and 15 build on this.

**Check the output:** AI tools often miscount days between dates, especially across month ends. Your spreadsheet's date math is the source of truth, not the AI.

---

## 14. Compare local vendors on reliability and variability

**The problem:** two vendors both promise fast delivery, but one keeps you guessing, and you need to know which to lean on.

**Rating rules (plain words, out of the last 4-5 orders):**

| Rating | Reliability (late orders) | Variability (longest actual days − shortest actual days) |
|---|---|---|
| **LOW** concern | Late 0-1 times | 0-1 days of spread |
| **MEDIUM** concern | Late 2 times | 2-3 days of spread |
| **HIGH** concern | Late 3 or more times | 4 or more days of spread |

Adjust these to fit your business. A cafe getting daily milk may treat 1 day late as serious; a contractor waiting on special-order fixtures may not.

**Prompt**
```
ROLE: You are a fair, practical vendor reviewer for a small [type of business]. Use plain words and simple arithmetic only.
CONTEXT: I rate vendors LOW, MEDIUM or HIGH concern using these rules, based on the last [4-5] orders:
- Reliability: late 0-1 times = LOW; 2 times = MEDIUM; 3 or more = HIGH.
- Variability: spread (longest actual_days minus shortest actual_days) of 0-1 days = LOW; 2-3 days = MEDIUM; 4 or more = HIGH.
DATA (CSV lead-time log: order_id, vendor, item, order_date, promised_date, received_date):
[paste rows]
TASK: For each vendor: 1) list actual_days and days_late for each order; 2) count late orders; 3) give the shortest, longest and spread of actual_days; 4) give the worst lateness; 5) rate reliability and variability with my rules; 6) give an overall rating (the higher of the two) and a one-line reason.
FORMAT: Table: Vendor | Orders | Late | Shortest / longest actual days | Spread | Worst lateness | Reliability | Variability | Overall | Reason. Then a confidence note for any vendor with fewer than 4 orders.
RULES: Use only my log. Show the math for each vendor in one line. Don't guess why a vendor was late.
```

**Workflow**
1. Paste your lead-time log (use case 13).
2. Run the prompt.
3. Check each vendor's late count and spread against your sheet.
4. Talk to any vendor rated HIGH before changing anything. Ask what's causing it.
5. Re-run every month or so. Note whether ratings improve.

**Check the output:** a few late orders can come from one bad week (weather, a sick driver). With fewer than 4 orders, any rating is a low-confidence guess. Ratings are only as good as the dates you logged.

---

## 15. Plan around lead times

**The problem:** you know a vendor is slow or unpredictable, but you still order as if every delivery will show up on time.

**Key ideas, in plain words:**
- **Reorder timing:** for a vendor with ups and downs, plan with their **longest** recent actual lead time, not the promised one. (See the reorder point in [use case 6](03-inventory-and-ordering.md).)
- **Buffer stock:** a little extra kept on hand for the days a delivery runs late. A simple size: what you use per day × the worst recent lateness. For items that spoil fast, a backup vendor may beat a big buffer.
- **Backup vendor:** a second place you've already tested ([use case 2](02-sourcing-and-suppliers.md)) that you can call when the first one slips.
- **Seasonal and holiday slowdowns:** many vendors close or slow down around holidays, harvest, or busy tourist weeks. Ask each vendor for their schedule ahead of time.

**Prompt**
```
ROLE: You are a planning helper for a small [type of business]. Plain words and simple arithmetic only.
CONTEXT: Here is my vendor summary (from my lead-time log) and how much I use per day. Coming holidays or slow periods I know about: [list, or "none"]. Items that spoil quickly: [list].
DATA (CSV: vendor, item, use per day, promised days, longest recent actual days, worst lateness in days, backup vendor yes/no):
[paste rows]
TASK: For each item: 1) suggest when to reorder, using the longest recent actual days (reorder point = use per day x longest actual days); 2) suggest a buffer (use per day x worst lateness) and say if that's sensible for a perishable item; 3) say whether a backup vendor matters more than a buffer; 4) list what to do before each holiday or slow period I named.
FORMAT: Table: Item | Vendor | Reorder point | Buffer | Backup needed? | Holiday note. Show the math in one line per item. Then a short checklist for the next holiday.
RULES: Use only my numbers. Don't name real vendors. Say clearly where a buffer would be too big to store or would spoil.
```

**Workflow**
1. Take your ratings from use case 14 and your daily use numbers.
2. Add the holidays and slow periods you know about.
3. Run the prompt.
4. Check each reorder point and buffer with a calculator.
5. Decide per item: bigger buffer, earlier ordering, or a backup vendor.
6. Before each holiday, ask vendors for their schedule and order earlier if needed.

**Check the output:** the AI doesn't know your storage space, shelf life or cash on hand. It also doesn't know vendor holiday schedules; get those from the vendor directly.

---

## Sample lead-time log (fictional restaurant, 10 orders)

A copy is in [sample-data/vendor-lead-time-log.csv](sample-data/vendor-lead-time-log.csv).

```
order_id,vendor,item,order_date,promised_date,received_date
1,Vendor A,Produce box,2026-09-01,2026-09-03,2026-09-03
2,Vendor A,Produce box,2026-09-08,2026-09-10,2026-09-10
3,Vendor A,Produce box,2026-09-15,2026-09-17,2026-09-18
4,Vendor A,Produce box,2026-09-22,2026-09-24,2026-09-24
5,Vendor B,Milk and cream,2026-09-01,2026-09-02,2026-09-02
6,Vendor B,Milk and cream,2026-09-08,2026-09-09,2026-09-12
7,Vendor B,Milk and cream,2026-09-15,2026-09-16,2026-09-16
8,Vendor B,Milk and cream,2026-09-22,2026-09-23,2026-09-27
9,Vendor C,Takeout containers,2026-09-02,2026-09-09,2026-09-07
10,Vendor C,Takeout containers,2026-09-16,2026-09-23,2026-09-23
```

### Worked example (fictional)

**Use case 13, days worked out:**

| Order | Vendor | Promised days | Actual days | Days late |
|---|---|---|---|---|
| 1 | Vendor A | 2 | 2 | 0 |
| 2 | Vendor A | 2 | 2 | 0 |
| 3 | Vendor A | 2 | 3 | 1 |
| 4 | Vendor A | 2 | 2 | 0 |
| 5 | Vendor B | 1 | 1 | 0 |
| 6 | Vendor B | 1 | 4 | 3 |
| 7 | Vendor B | 1 | 1 | 0 |
| 8 | Vendor B | 1 | 5 | 4 |
| 9 | Vendor C | 7 | 5 | −2 (early) |
| 10 | Vendor C | 7 | 7 | 0 |

Example: order 8 was placed Sept 22 and arrived Sept 27, so 27 − 22 = **5 actual days**; it was promised Sept 23, so 27 − 23 = **4 days late**.

**Use case 14, vendor comparison:**

| Vendor | Orders | Late | Shortest / longest | Spread | Worst lateness | Reliability | Variability | Overall |
|---|---|---|---|---|---|---|---|---|
| Vendor A (produce) | 4 | 1 | 2 / 3 days | 1 day | 1 day | LOW | LOW | **LOW** |
| Vendor B (dairy) | 4 | 2 | 1 / 5 days | 4 days | 4 days | MEDIUM | HIGH | **HIGH** |
| Vendor C (containers) | 2 | 0 | 5 / 7 days | 2 days | 0 (once early) | LOW | MEDIUM | **MEDIUM** (low confidence: only 2 orders) |

Reason for Vendor B: promises next-day delivery, but 2 of 4 orders took 4-5 days. The promise isn't something to plan on.

**Use case 15, planning:**
- *Vendor B, milk and cream:* the restaurant uses about 3 gallons a day. Reorder point using the longest recent actual time: 3 × 5 = **15 gallons**. Buffer for the worst lateness: 3 × 4 = **12 gallons**, which is a lot of milk to store before it goes bad. Better plan: line up a backup dairy option and test it, and talk to Vendor B about the late weeks.
- *Vendor A, produce:* steady. Keep ordering as usual with a 1-day cushion.
- *Vendor C, containers:* doesn't spoil, so a buffer is easy. Before a holiday week, order a week earlier and ask about their closing days.

### Verify the AI's results against the log
- [ ] Add **actual_days** in column G: `=F2-D2` (received − ordered). Format the column as a plain number.
- [ ] Add **days_late** in column H: `=F2-E2` (received − promised).
- [ ] Count late orders per vendor: `=COUNTIFS(B:B,"Vendor B",H:H,">0")`. Vendor B should show 2.
- [ ] Find the spread per vendor: sort by vendor, then read the shortest and longest actual_days by eye (or use MINIFS / MAXIFS).
- [ ] Compare every number in the AI's table with your sheet. Fix or drop anything that doesn't match.

**Check the output:** in this sample, the most common AI mistakes would be counting days across dates wrong, or rating Vendor C with confidence from only 2 orders. The log is the source of truth.

---

Next: [Risk, disruption and records](06-risk-disruption-and-records.md) · Back to [overview](01-overview-and-guardrails.md)

---

Back to [README](README.md)

Rashon Alsberry, independent portfolio project - [starboy1968.github.io](https://starboy1968.github.io)
