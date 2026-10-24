# Worked Example 1: A Small Cafe's Weekly Stock (Waste and Par Levels)

Part of the [use cases](README.md) for [Localized Small Supply Chain](../README.md). Uses prompts from [use case 12](../04-forecasting-overstock-and-dead-stock.md), [use case 7](../03-inventory-and-ordering.md) and [use case 5](../03-inventory-and-ordering.md).

> **Fictional.** Juniper Cafe, its suppliers and every number are made up to show the method. The AI output below is an **illustrative example** of what a good answer looks like, not output from a real tool run.

---

## The situation
Juniper Cafe is a small coffee shop with one delivery a week from each supplier. The owner has two complaints:
- "We keep running out of oat milk and bagels."
- "I throw out croissants and spinach every week."

The owner keeps a simple weekly stock sheet (4 weeks, 5 items) and wants to know what's going wrong and what to order next week.

## Sample input: the stock sheet
File: [sample-data/juniper-cafe-stock-sheet.csv](../sample-data/juniper-cafe-stock-sheet.csv)

```csv
week,item,unit,start,received,used_or_sold,wasted,end,ran_out,supplier
W1,Oat milk,carton,2,12,14,0,0,yes,Supplier A
W2,Oat milk,carton,0,12,12,0,0,yes,Supplier A
W3,Oat milk,carton,0,12,12,0,0,yes,Supplier A
W4,Oat milk,carton,0,12,12,0,0,yes,Supplier A
W1,Whole milk,gallon,3,18,17,1,3,no,Supplier A
W2,Whole milk,gallon,3,18,18,0,3,no,Supplier A
W3,Whole milk,gallon,3,18,16,1,2,no,Supplier A
W4,Whole milk,gallon,2,18,17,1,2,no,Supplier A
W1,Croissants (frozen),each,20,60,52,8,20,no,Supplier B
W2,Croissants (frozen),each,20,60,50,9,21,no,Supplier B
W3,Croissants (frozen),each,21,60,54,7,20,no,Supplier B
W4,Croissants (frozen),each,20,60,51,8,21,no,Supplier B
W1,Spinach,lb,1,8,5,3,1,no,Supplier C
W2,Spinach,lb,1,8,6,2,1,no,Supplier C
W3,Spinach,lb,1,8,5,3,1,no,Supplier C
W4,Spinach,lb,1,8,5,3,1,no,Supplier C
W1,Bagels,dozen,2,10,10,1,1,no,Supplier B
W2,Bagels,dozen,1,10,11,0,0,yes,Supplier B
W3,Bagels,dozen,0,10,10,0,0,yes,Supplier B
W4,Bagels,dozen,0,10,9,1,0,yes,Supplier B
```

## Which prompts to use, in order
1. **Find patterns first:** the "Paste a spreadsheet" prompt from [use case 12](../04-forecasting-overstock-and-dead-stock.md). It checks that each row adds up and flags run-outs, build-ups and waste.
2. **Dig into waste:** the "Track spoilage and waste" prompt from [use case 7](../03-inventory-and-ordering.md), if you also keep a waste log with reasons.
3. **Set next week's order:** the "Set par levels" prompt from [use case 5](../03-inventory-and-ordering.md). Fill in: deliveries every **7** days, cushion of **about 2-3 days**.

## How to give the AI the data
- [ ] Run the privacy check from use case 12 (no customer, staff or payment details; supplier names as letters).
- [ ] **Paste:** copy the CSV text above (or select the rows in your spreadsheet and copy) and paste it under the prompt's **DATA** line.
- [ ] **Or upload:** if your AI tool accepts file uploads, attach the CSV and write "see attached file" under DATA. The prompt stays the same.
- [ ] Fill in the CONTEXT line, for example: "Things I know about: we added an oat milk latte special in W1."

## Sample AI output (illustrative example)

> *Illustrative example of a good answer. A real tool's answer will differ, and may contain mistakes.*

**Table A: Rows that don't add up**

| Week | Item | Expected end | Recorded end |
|---|---|---|---|
| W3 | Whole milk | 3 + 18 − 16 − 1 = 4 | 2 |

**Table B: Patterns**

| Item | Pattern | Evidence (rows and numbers) | Confidence | Suggested next step |
|---|---|---|---|---|
| Oat milk | Runs out every week | ran_out = yes in W1-W4; end = 0 every week; all 12 received are used | HIGH | Raise the order. Real demand is unknown because you sold out, so tally "asked but out" for a week. |
| Bagels | Runs out most weeks | ran_out = yes in W2-W4; used 10, 11, 10, 9 of about 10 available | MEDIUM | Try ordering 12 dozen for two weeks and watch for sell-outs. |
| Croissants | Steady waste and leftover stock | Wasted 8, 9, 7, 8 (32 in 4 weeks, about 8 a week); about 20 left at every week's end | HIGH | Bake about 1 fewer per day; order less so the extra 20 doesn't sit in the freezer. |
| Spinach | Steady waste | Wasted 3, 2, 3, 3 lb (11 lb) while using 5, 6, 5, 5 lb (21 lb) | HIGH | Order less, or ask about two smaller deliveries a week. |
| Whole milk | Steady, about right | Used 17, 18, 16, 17; never ran out | MEDIUM | No change, but fix the W3 count first. |

**Suggested par levels (use case 5)**

| Item | Avg use per week | Cushion | Suggested par | On hand now | Order next week |
|---|---|---|---|---|---|
| Oat milk | at least 12.5 (50 ÷ 4), true demand unknown | 3 | 15 | 0 | 15 |
| Whole milk | 17 (68 ÷ 4) | 2 | 19 | 2 | 17 |
| Croissants | about 52 (207 ÷ 4) | 4 | 56 | 21 | 35 |
| Spinach | about 5 (21 ÷ 4 = 5.25) | 1 | 7 (rounded up) | 1 | 6 |
| Bagels | 10 (40 ÷ 4), true demand unknown | 2 | 12 | 0 | 12 |

**What I can't tell from this data**
- How much oat milk and how many bagels you *could* have sold if you hadn't run out.
- Why spinach is wasted (spoiled, over-prepped, or a menu item that didn't sell).
- Whether W3 whole milk is a counting mistake or 2 gallons of unrecorded waste.

## Human check: what to verify
- [ ] **Fix the data first.** Recount or ask staff about W3 whole milk before trusting the milk pattern.
- [ ] **Re-add one row per item yourself:** start + received − used − wasted = end.
- [ ] **Re-do two averages by hand,** for example croissants: 52 + 50 + 54 + 51 = 207; 207 ÷ 4 ≈ 52.
- [ ] **Check the "ran out" flags** against what staff remember. Did oat milk run out on Friday or on Monday?
- [ ] **Sanity-check the croissant cut.** Dropping the order from 60 to 35 is big. Is the freezer full of 20 extra, or were those already baked?
- [ ] **Food safety:** holding times and storage rules come from your local health rules, not the AI.

## What to do next
- [ ] Order the suggested amounts for one week, with oat milk and bagels raised.
- [ ] Keep a tally sheet for "asked for oat milk / bagels but we were out."
- [ ] Start a short waste log with reasons for croissants and spinach ([use case 7](../03-inventory-and-ordering.md)).
- [ ] Ask Supplier C if spinach can come twice a week in smaller amounts.
- [ ] Re-run the same prompt after 2 more weeks and compare.

---

Next: [Worked example 2: retail forecasting, overstock and dead stock](retail-forecast-overstock-dead-stock.md) · Back to [use cases](README.md)
