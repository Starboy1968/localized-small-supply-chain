# Worked Example 3: A Buyer Comparing Local Vendors' Lead Times and Reliability

Part of the [use cases](README.md) for [Localized Small Supply Chain](../README.md). Uses prompts from [use cases 13, 14 and 15](../05-supplier-lead-times.md).

> **Fictional.** Little Pine Deli, Vendors D, E and F, and every date are made up to show the method. The AI output below is an **illustrative example** of what a good answer looks like, not output from a real tool run.

---

## The situation
Little Pine Deli orders from three local vendors every Monday. The buyer feels "the cheese guy is always late" and "containers are hit or miss," but has no proof. They kept a delivery log for 5 weeks and want to know:
- Which vendor is least reliable (often late)?
- Which is least predictable (delivery time jumps around)?
- When should each item be reordered, and is a backup vendor needed before the holidays?

## Sample input: the delivery log
File: [sample-data/little-pine-deli-delivery-log.csv](../sample-data/little-pine-deli-delivery-log.csv)

```csv
order_id,vendor,item,order_date,promised_date,received_date,received_in_full
1,Vendor D,Sandwich bread,2026-09-07,2026-09-08,2026-09-08,yes
2,Vendor D,Sandwich bread,2026-09-14,2026-09-15,2026-09-15,yes
3,Vendor D,Sandwich bread,2026-09-21,2026-09-22,2026-09-22,yes
4,Vendor D,Sandwich bread,2026-09-28,2026-09-29,2026-09-30,yes
5,Vendor D,Sandwich bread,2026-10-05,2026-10-06,2026-10-06,yes
6,Vendor E,Sliced cheese,2026-09-07,2026-09-10,2026-09-10,yes
7,Vendor E,Sliced cheese,2026-09-14,2026-09-17,2026-09-20,no
8,Vendor E,Sliced cheese,2026-09-21,2026-09-24,2026-09-24,yes
9,Vendor E,Sliced cheese,2026-09-28,2026-10-01,2026-10-03,no
10,Vendor E,Sliced cheese,2026-10-05,2026-10-08,2026-10-09,yes
11,Vendor F,Takeout containers,2026-09-07,2026-09-12,2026-09-11,yes
12,Vendor F,Takeout containers,2026-09-14,2026-09-19,2026-09-19,yes
13,Vendor F,Takeout containers,2026-09-21,2026-09-26,2026-09-25,yes
14,Vendor F,Takeout containers,2026-09-28,2026-10-03,2026-10-07,yes
15,Vendor F,Takeout containers,2026-10-05,2026-10-10,2026-10-10,yes
```

The `received_in_full` column is an optional extra on top of the use case 13 log: "yes" if everything ordered arrived.

## Which prompts to use, in order
1. **Compare vendors:** "Compare local vendors on reliability and variability" from [use case 14](../05-supplier-lead-times.md). Use the last **5** orders. Add to TASK: "Also count orders not received in full."
2. **Plan around them:** "Plan around lead times" from [use case 15](../05-supplier-lead-times.md). Daily use the buyer knows: bread 30 loaves, cheese 3 lb, containers 4 sleeves. Perishable: bread, cheese. Coming slow period: Thanksgiving week.

## How to give the AI the data
- [ ] Use vendor letters or names only, with no contact details or account numbers.
- [ ] **Paste:** copy the CSV text and paste it under the prompt's **DATA** line.
- [ ] **Or upload:** attach the CSV if your tool allows uploads, and write "see attached file" under DATA. The prompt stays the same.
- [ ] For use case 15, type the small summary table from step 1's answer (after you've checked it) into the DATA line.

## Sample AI output (illustrative example)

> *Illustrative example of a good answer. A real tool's answer will differ, and may contain mistakes.*

**1) Vendor comparison (use case 14)**

| Vendor | Orders | Late | Shortest / longest actual days | Spread | Worst lateness | Not in full | Reliability | Variability | Overall | Reason |
|---|---|---|---|---|---|---|---|---|---|---|
| D (bread) | 5 | 1 | 1 / 2 | 1 | 1 day | 0 | LOW | LOW | **LOW** | One order a day late; otherwise on time |
| E (cheese) | 5 | 3 | 3 / 6 | 3 | 3 days | 2 | HIGH | MEDIUM | **HIGH** | Late 3 of 5 times, and short twice |
| F (containers) | 5 | 1 | 4 / 9 | 5 | 4 days | 0 | LOW | HIGH | **HIGH** | Usually on time or early, but one order took 9 days |

*Math, one line each:*
- D: actual days 1, 1, 1, 2, 1. Late: order 4 (+1). Spread 2 − 1 = 1.
- E: actual days 3, 6, 3, 5, 4. Late: order 7 (+3), order 9 (+2), order 10 (+1). Spread 6 − 3 = 3.
- F: actual days 4, 5, 4, 9, 5. Late: order 14 (+4). Early: orders 11 and 13 (1 day each). Spread 9 − 4 = 5.

*Confidence:* 5 orders each is enough for a first look, not a final verdict.

**2) Planning (use case 15)**

| Item | Vendor | Reorder point | Buffer | Backup needed? | Holiday note |
|---|---|---|---|---|---|
| Sandwich bread | D | 30 × 2 = 60 loaves | 30 × 1 = 30 loaves, but bread goes stale fast, so keep the buffer small | Nice to have | Ask about holiday bake schedule |
| Sliced cheese | E | 3 × 6 = 18 lb | 3 × 3 = 9 lb, if shelf life and fridge space allow | **Yes** | Order earlier the week before Thanksgiving |
| Takeout containers | F | 4 × 9 = 36 sleeves | 4 × 4 = 16 sleeves; they don't spoil, so a buffer works if you have room | Optional | Order a week early before Thanksgiving |

**Holiday checklist**
- [ ] Ask D, E and F for their Thanksgiving-week delivery days.
- [ ] Place the cheese and container orders a week earlier than usual.
- [ ] Have a tested backup for cheese before then.

## Human check: what to verify
- [ ] **Re-count late orders per vendor** from the log (received date after promised date).
- [ ] **Re-do actual days for 2-3 orders** by subtracting dates, for example order 7: Sep 14 to Sep 20 = 6 days.
- [ ] **Check the one-off.** Was F's 9-day order (order 14) a single bad week (weather, a holiday, a stock-out)? Ask F before calling them unreliable.
- [ ] **Short deliveries:** check the two invoices for orders 7 and 9. How much was missing?
- [ ] **Storage and shelf life:** confirm you can actually store 16 extra sleeves and 9 extra lb of cheese safely. The AI can't see your fridge or storeroom.
- [ ] **Don't drop a vendor on the AI's say-so.** Talk to Vendor E first and share the dates.

## What to do next
- [ ] Share the log with Vendor E and ask what's causing late and short deliveries.
- [ ] Find and test one backup cheese supplier ([use case 2](../02-sourcing-and-suppliers.md)) with a small trial order.
- [ ] Put the new reorder points on shelf labels (for example, "Order cheese at 18 lb").
- [ ] Keep logging every order and re-run the comparison monthly.

---

Previous: [Worked example 2: retail forecasting](retail-forecast-overstock-dead-stock.md) · Back to [use cases](README.md)
