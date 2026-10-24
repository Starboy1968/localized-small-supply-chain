# Inventory and Ordering

Part of [Localized Small Supply Chain: AI Prompts and Workflows](01-overview-and-guardrails.md). Use cases 5-8.

All examples are **fictional**. The math stays at "add, subtract, multiply." Every prompt is plain text and works in any AI chat tool.

**See it end to end:** [Worked example 1: a small cafe's weekly stock](use-cases/cafe-weekly-stock.md) (use cases 5 and 7).

---

## 5. Set par levels

**The problem:** you order by gut feel, so some weeks you run out and other weeks the shelf is crammed.

**Par level, in plain words:** how much you want on hand right after a delivery: enough to last until the next delivery, plus a small cushion.

**Simple math:** par = what you use between deliveries + a cushion. Order amount = par − what's on hand now.

**Prompt**
```
ROLE: You are an inventory helper for a small [type of business].
CONTEXT: I get deliveries every [number] days. I want a small cushion of about [amount or "a few days"] in case a delivery is late.
DATA (CSV: item, unit, typical use per week, on hand now):
[paste rows]
TASK: Suggest a par level for each item and how much to order today.
FORMAT: A table: Item | Unit | Use between deliveries | Cushion | Suggested par | On hand | Order today. Show the simple math for each row.
RULES: Use only my numbers. If an item's use looks odd or is missing, flag it instead of guessing.
```

**Workflow**
1. List your top 10-20 items with typical use per week (from counts or sales).
2. Run the prompt.
3. Check 2-3 rows by hand.
4. Write the par on the shelf label or in your order sheet.
5. Review pars each month, and before a busy season.

**Worked example (fictional):** a cafe uses about 10 lb of coffee beans a week, gets a delivery once a week, and wants a 3 lb cushion. Par = 10 + 3 = **13 lb**. With 4 lb on hand, order 13 − 4 = **9 lb**.

**Check the output:** the AI doesn't know about the catering order next Tuesday. Adjust the par for anything unusual you know about.

---

## 6. Reorder points in plain words

**The problem:** for items you order "when needed" (not on a fixed day), you notice too late.

**Reorder point, in plain words:** "When I get down to this many, order now." It's what you'll use while waiting for the delivery, plus a cushion.

**Simple math:** reorder point = daily use × (days to deliver + cushion days).

**Prompt**
```
ROLE: You are an inventory helper for a small [type of business].
CONTEXT: I order these items whenever they run low, not on a schedule.
DATA (CSV: item, unit, use per day, days from order to delivery):
[paste rows]
TASK: For each item, give a reorder point with a cushion of [number] days. Then write a one-line shelf note, like "Order when 16 left."
FORMAT: A table: Item | Use per day | Days to deliver | Cushion days | Reorder point | Shelf note. Show the math.
RULES: Use only my numbers. Point out any item where the delivery time is long compared with how fast I use it.
```

**Workflow**
1. For each item, note how much you use per day and how long delivery takes (see [use case 13](05-supplier-lead-times.md) for tracking lead times).
2. Run the prompt.
3. Check the math on a couple of rows.
4. Put the shelf note on the bin, box or shelf.
5. Update when delivery times change.

**Worked example (fictional):** a farm stand uses about 4 sleeves of berry clamshells a day. The online seller takes 3 days, and the owner wants a 1-day cushion. Reorder point = 4 × (3 + 1) = **16 sleeves**. Shelf note: "Order when 16 left."

**Check the output:** daily use isn't steady for a farm stand (rain, holidays, harvest). The AI can't see the weather. Raise the cushion in peak weeks.

---

## 7. Track spoilage and waste

**The problem:** you throw things out every day but don't know which items, how much, or why.

**Prompt**
```
ROLE: You are a waste-reduction helper for a small [type of business].
CONTEXT: I logged what I threw out for [number] days, with a reason.
DATA (CSV: date, item, amount, unit, reason such as expired, damaged, over-prepped, returned):
[paste rows]
TASK: Group the waste by item and by reason. Point out the top 3 items and their most common reason. Suggest one small, low-risk change to try for each.
FORMAT: 1) Table: Item | Total wasted | Most common reason. 2) Three suggestions, one line each.
RULES: Use only my log. Don't estimate money unless I gave costs. Keep suggestions small and easy to undo.
```

**Workflow**
1. Keep a waste log for 1-2 weeks (a clipboard or a shared sheet is enough).
2. Paste it into the prompt.
3. Re-add the top item's total yourself.
4. Try one small change for 2 weeks (for example, prep less of one item).
5. Log again and compare.

**Worked example (fictional):** a cafe bakes 12 croissants a day, sells about 9, and throws out about 3, so about 3 × 7 = **21** in a week. The AI's suggestion: bake 10 for two weeks and watch for sell-outs. The owner tries it, and logs sell-out times.

**Check the output:** food-safety and holding-time rules come from your local health rules, not the AI. The AI also can't tell if an item was wasted because of a fridge problem.

---

## 8. Turn POS sales data into an order list

**The problem:** your register (POS, point of sale) knows exactly what sold, but you still write the order from memory.

**Prompt**
```
ROLE: You are an ordering helper for a small [type of business].
CONTEXT: Below is a sales export by item from my POS for [time period], plus what's on hand now and my par levels.
DATA (CSV: item, units sold, on hand now, par level, supplier):
[paste rows, with customer and payment columns deleted first]
TASK: Make an order list. For each item, order amount = par level minus on hand (zero if on hand is already at or above par). Group the list by supplier.
FORMAT: One table per supplier: Item | On hand | Par | Order. Then a short list of items that sold much more or less than usual.
RULES: Use only my numbers. Flag any row that looks wrong (for example, negative on hand).
```

**Workflow**
1. Export item sales from your POS as CSV (most systems have an export or report).
2. Delete any customer, card or staff columns before pasting.
3. Add on-hand counts and pars.
4. Run the prompt, then check 3 rows by hand.
5. Place orders yourself.

**Worked example (fictional):** a small gift shop.

| Item | On hand | Par | Order |
|---|---|---|---|
| Soy candle, large | 20 | 48 | 48 − 20 = **28** |
| Ceramic mug | 30 | 36 | 36 − 30 = **6** |
| Greeting cards (pack) | 26 | 24 | Above par: **0** |

**Check the output:** POS counts drift from what's on the shelf (breakage, theft, miscounts). Do a quick shelf count of anything big before ordering.

---

Next: [Forecasting, overstock and dead stock](04-forecasting-overstock-and-dead-stock.md) · Back to [overview](01-overview-and-guardrails.md)

---

Back to [README](README.md)

Rashon Alsberry, independent portfolio project - [starboy1968.github.io](https://starboy1968.github.io)
