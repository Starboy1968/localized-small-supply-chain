# Worked Example 2: A Local Retailer's Forecast, Overstock and Dead Stock

Part of the [use cases](README.md) for [Localized Small Supply Chain](../README.md). Uses prompts from [use cases 9, 10 and 11](../04-forecasting-overstock-and-dead-stock.md).

> **Fictional.** Fern & Twine, a small gift shop, and every number are made up to show the method. The AI output below is an **illustrative example** of what a good answer looks like, not output from a real tool run.

---

## The situation
Fern & Twine sells candles, mugs, kitchen linens, seasonal items and cards. It's October 1, 2026. The owner wants to know three things before placing holiday orders:
- What will we likely sell in October?
- Which items do we have too much of (overstock)?
- What hasn't sold in ages (dead stock)?

The shop's goal is about **6 weeks of stock** for most items. Its dead-stock rule is **no sale in 90 days**.

## Sample input: the sales history
File: [sample-data/fern-twine-sales-history.csv](../sample-data/fern-twine-sales-history.csv). Monthly units sold, April to September 2026, with units on hand and cost per unit as of October 1.

```csv
item,unit_cost,on_hand,apr,may,jun,jul,aug,sep,last_sale_date,season_end
Soy candle - lavender,6,30,20,22,18,21,19,20,2026-09-30,none
Soy candle - pumpkin spice,6,90,0,0,0,2,10,24,2026-09-30,2026-11-30
Ceramic mug,5,60,12,10,11,9,10,8,2026-09-28,none
Linen tea towel,4,40,6,4,3,2,1,0,2026-08-19,none
Beach tote,7,25,0,0,0,0,0,0,2026-02-14,none
Wool socks,8,12,3,1,0,2,6,15,2026-09-30,2026-02-28
Greeting cards - assorted,1,150,40,38,42,36,44,40,2026-09-30,none
```

## Which prompts to use, in order
1. **Forecast:** "Forecast demand in plain words" from [use case 9](../04-forecasting-overstock-and-dead-stock.md). Coming period: October. Things I know: "holiday shopping starts mid-November; a street fair on Oct 17."
2. **Overstock:** "Spot and fix overstock" from [use case 10](../04-forecasting-overstock-and-dead-stock.md). Target: 6 weeks. Items that expire or go out of season: pumpkin spice candle (Nov 30), wool socks (end of Feb).
3. **Dead stock:** "Find and clear dead stock" from [use case 11](../04-forecasting-overstock-and-dead-stock.md). Rule: 90 days. Today's date: 2026-10-01.

**Simple conversion:** the prompts ask for *weekly* use. Monthly average ÷ 4 is close enough for this check. Say so in the CONTEXT line so the AI does the same.

## How to give the AI the data
- [ ] Remove anything you don't need: no customer names, card data, or staff details.
- [ ] **Paste:** copy the CSV text and paste it under the prompt's **DATA** line.
- [ ] **Or upload:** attach the CSV if your tool allows uploads, and write "see attached file" under DATA. The prompt stays the same.
- [ ] Run the three prompts one at a time, in the same chat or separate chats. Paste the data each time if you start a new chat.

## Sample AI output (illustrative example)

> *Illustrative example of a good answer. A real tool's answer will differ, and may contain mistakes.*

**1) October starting guess (use case 9)**

| Item | Recent average (6 months) | Seasonal note | Starting guess for Oct (low / likely / high) |
|---|---|---|---|
| Soy candle - lavender | 20 a month (120 ÷ 6) | Very steady | 18 / 20 / 24 |
| Soy candle - pumpkin spice | 6 a month (36 ÷ 6), but rising: 2, 10, 24 | Seasonal; no last-year data | 20 / 30 / 40 (LOW confidence) |
| Wool socks | 4.5 a month (27 ÷ 6), but rising: 2, 6, 15 | Seasonal; no last-year data | 12 / 18 / 25 (LOW confidence) |
| Greeting cards | 40 a month (240 ÷ 6) | Steady | 36 / 40 / 46 |

*Reasoning:* steady items use the 6-month average. For rising seasonal items, the 6-month average is misleading, so the guess starts from September and assumes the climb continues a little. Without last year's numbers, these are rough. The street fair may add a bump.

**2) Overstock (use case 10), target 6 weeks**

| Item | On hand | Weekly use (monthly avg ÷ 4) | Weeks of cover | Extra units | Suggested options |
|---|---|---|---|---|---|
| Soy candle - pumpkin spice | 90 | 6 (Sep 24 ÷ 4) | 15 | about 36 by Nov 30* | Pause reorders; bundle with a mug; feature at the street fair |
| Ceramic mug | 60 | 2.5 (10 ÷ 4) | 24 | 45 (60 − 15) | Pause the next reorder; bundle with a candle as a gift set |
| Greeting cards | 150 | 10 (40 ÷ 4) | 15 | 90 (150 − 60) | Pause the next reorder; cards don't spoil, so lower priority |
| Soy candle - lavender | 30 | 5 (20 ÷ 4) | 6 | 0 | On target, no action |
| Wool socks | 12 | about 4 (15 ÷ 4) | about 3 | none; **may run short** | Consider a reorder soon (see forecast) |

*\*Pumpkin spice: the season ends Nov 30, about 9 weeks away. At 6 a week, about 54 would sell, leaving about 90 − 54 = 36. If October sales climb as forecast, fewer will be left. Listed first because of the season end.*

**3) Dead stock (use case 11), rule 90 days**

| Item | Days since last sale | Units | Cash tied up | Suggested options |
|---|---|---|---|---|
| Beach tote | 229 (Feb 14 to Oct 1) | 25 | 25 × $7 = **$175** | Bundle free with orders over a set amount; sell at the street fair; donate (check with a tax professional on any write-off) |

**Watch list (not dead yet):** Linen tea towel, 43 days since last sale, sales falling 6, 4, 3, 2, 1, 0. Cash tied up: 40 × $4 = $160. Stop reordering for now.

**What to stop doing:** reordering mugs, cards and tea towels on autopilot.

**What I can't tell from this data:** last year's holiday sales, margins, supplier return rules, or whether beach totes might sell next summer.

## Human check: what to verify
- [ ] **Re-do "units × cost" for every dead or overstock item.** One easy slip to watch for: using the wrong row's cost (for example $4 from the tea towel row instead of $7 for the tote).
- [ ] **Re-add two monthly totals** yourself (for example mugs: 12 + 10 + 11 + 9 + 10 + 8 = 60).
- [ ] **Check the seasonal guesses against memory or old receipts.** Did pumpkin spice and socks sell more last October? If you have last year's numbers, add them and re-run use case 9.
- [ ] **Beach tote:** it sold nothing even in June-August, so "it'll sell next summer" is unlikely. That supports calling it dead.
- [ ] **Supplier return rules:** check directly with the supplier before planning a return.
- [ ] **Donations and write-offs:** ask a tax professional, not the AI.

## What to do next
- [ ] Pause reorders for mugs, cards, tea towels and pumpkin spice candles.
- [ ] Put a candle-and-mug gift set out front before the street fair.
- [ ] Decide on beach totes by a set date (for example, Nov 1): bundle, market table, or donate.
- [ ] Place a small wool sock reorder if the supplier's lead time is long.
- [ ] Lower par levels for the overstocked items ([use case 5](../03-inventory-and-ordering.md)) so the build-up doesn't repeat.
- [ ] In November, compare October's real sales with the starting guess.

---

Previous: [Worked example 1: cafe weekly stock](cafe-weekly-stock.md) · Next: [Worked example 3: vendor lead times](vendor-lead-times-reliability.md) · Back to [use cases](README.md)
