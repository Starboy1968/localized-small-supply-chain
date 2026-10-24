# Risk, Disruption and Records

Part of [Localized Small Supply Chain: AI Prompts and Workflows](01-overview-and-guardrails.md). Use cases 16-19.

All examples are **fictional**. Risk is rated LOW / MEDIUM / HIGH in plain words, with no scoring formulas. The goal is defensive: notice weak spots early and have a plan ready. Every prompt is plain text and works in any AI chat tool.

---

## 16. Check for single-supplier dependence

**The problem:** some of your key items come from just one place, and you won't notice until that place has a bad week.

**Single point of failure, in plain words:** one supplier, item or person that, if lost, stops part of the business.

**Prompt**
```
ROLE: You are a supply risk helper for a small [type of business]. Use plain words and LOW / MEDIUM / HIGH ratings, no formulas.
CONTEXT: I want to know which items would hurt most if one supplier failed.
DATA (CSV: item, supplier, number of suppliers I've actually used for it, is there a substitute item (yes/no), how bad if I ran out for a week (small / annoying / serious)):
[paste rows]
TASK: Rate each item's dependence risk:
- HIGH = only one supplier AND no substitute AND running out would be serious.
- MEDIUM = only one supplier but a substitute exists, OR two suppliers but running out would be serious.
- LOW = two or more suppliers, or easy to substitute.
Then list the HIGH items first with one plain next step each.
FORMAT: Table: Item | Supplier(s) | Substitute? | Impact | Risk | Next step.
RULES: Use only my data. Don't suggest specific businesses. Note any item where two "different" suppliers might really get it from the same place (I'll check).
```

**Workflow**
1. List your top 10-20 items (start with the supplier list from [use case 1](02-sourcing-and-suppliers.md)).
2. Fill in the columns honestly. "Number of suppliers" means ones you've actually bought from, not ones you could call.
3. Run the prompt.
4. For each HIGH, start the backup-supplier workflow ([use case 2](02-sourcing-and-suppliers.md)).
5. Re-check every few months.

**Worked example (fictional):**

| Item | Supplier(s) | Substitute? | Impact | Risk | Next step |
|---|---|---|---|---|---|
| Wine bottles (winery) | Supplier A only | No | Serious: can't bottle | **HIGH** | Find and test a second bottle source before harvest |
| Labels | Supplier B only | Yes (local print shop) | Annoying | **MEDIUM** | Get a sample run from the print shop |
| Corks | Suppliers C and D | Yes | Annoying | **LOW** | No change; check C and D aren't the same maker |

**Check the output:** the AI can't see who your suppliers buy from. Two "different" suppliers can share the same factory or distributor. Ask them. (The case study [Two Suppliers, One Factory](https://github.com/Starboy1968/two-suppliers-one-factory) walks through this.)

---

## 17. Write a one-page disruption playbook

**The problem:** when a delivery doesn't come, a road closes or a storm hits, decisions get made in a panic.

**Disruption playbook, in plain words:** a one-page "if this happens, we do that" sheet, written on a calm day.

**Prompt**
```
ROLE: You are a planning helper for a small [type of business]. Defensive, practical, plain words.
CONTEXT: I want a one-page playbook for supply problems. My key items and their suppliers: [paste list]. My backup options so far: [paste list or "none yet"]. Who can make decisions: [roles, not names].
TASK: Write a one-page playbook for these situations: 1) a key delivery is late or missing; 2) a supplier runs out or closes; 3) bad weather or a road closure; 4) a price jumps suddenly; 5) a product recall or quality problem.
For each: first 3 steps, who does them (by role), what to tell customers if needed, and when to go back to normal.
FORMAT: One short section per situation with numbered steps. A top line: "Keep this printed near the phone."
RULES: Use only the suppliers and backups I gave. For recalls or safety issues, the first step is always to follow the official notice and stop using the product. Don't invent rules or phone numbers.
```

**Workflow**
1. Gather your supplier list and any backup options.
2. Run the prompt.
3. Read each situation with whoever helps you run the business. Fix anything that wouldn't really work.
4. Print it and keep it where people will see it.
5. After any real disruption, update the page with what you learned.

**Worked example (fictional):** a small contractor's playbook for "materials delivery late": 1) call the supplier for a new date; 2) check the backup supply yard for the same item; 3) tell the client the job may shift and by how much; 4) move crew to the next task that doesn't need the material. Back to normal when the delivery is confirmed in writing.

**Check the output:** the AI doesn't know your contracts, insurance or local rules. For recalls, food safety, medical supplies or anything legal, follow the official source, not the playbook draft.

---

## 18. Clean up master data (duplicate items and vendors)

**The problem:** the same item or vendor is entered three different ways, so counts, sales reports and orders don't add up.

**Master data, in plain words:** the basic records everything else depends on: item names, units, prices and vendor names. For example, a small winery's POS keeps the menu items and their prices. If those records are messy, every report built on them is messy too.

**Prompt**
```
ROLE: You are a careful data-cleanup helper for a small [type of business].
CONTEXT: My item list (or vendor list) has duplicates and inconsistent names, units and spellings.
DATA (CSV: id, name, unit, price, vendor):
[paste rows]
TASK: Find likely duplicates (same thing, different spelling or unit). Suggest one clean name and one standard unit for each group. Flag anything that looks like a duplicate but might not be (for example, a different size).
FORMAT: Table: Group | Rows (ids) | Suggested clean name | Standard unit | Why I think they match | Confidence (HIGH / MEDIUM / LOW).
RULES: Do not delete or merge anything; only suggest. Do not change prices. Use only my data.
```

**Workflow**
1. Export your item or vendor list from your POS, spreadsheet or inventory app.
2. Remove anything not needed (customer data, account numbers).
3. Run the prompt.
4. Review each group. Only you know if "Oat milk 1L" and "Oat Milk (barista)" are really the same product.
5. Make the changes yourself in the source system, one group at a time, and keep a copy of the old list.
6. Agree on a naming rule (for example: "Item, size, unit") so it stays clean.

**Worked example (fictional):**

| Group | Rows | Suggested name | Unit | Why | Confidence |
|---|---|---|---|---|---|
| 1 | 12, 47, 63 ("oat milk", "Oat Milk 1L", "OATMILK CTN") | Oat milk, 1 L carton | carton | Same item, different spellings | HIGH |
| 2 | 20 vs. 47 ("Oat Milk (barista)" vs. "Oat Milk 1L") | Check before merging | carton | Might be a different product line | LOW |
| 3 | Vendors 3, 9 ("Supplier A", "Supplier A LLC") | Supplier A | n/a | Same vendor, two entries | MEDIUM |

**Check the output:** the AI matches names by how they look, not by what's in the box. Never let it merge or delete records. Check against invoices and the product itself.

---

## 19. Draw a simple local supply map

**The problem:** you can't see, at a glance, who you depend on, how far away they are, and where a single problem could knock out several items.

**Supply map, in plain words:** a simple picture or table of your suppliers, what each provides, roughly where they are, and who they depend on (if you know).

**Prompt**
```
ROLE: You are a planning helper for a small [type of business]. Keep it simple and visual.
CONTEXT: I want a one-page map of my local supply chain.
DATA (CSV: supplier, what they supply, rough distance or area, how they deliver, who THEY get it from if known, backup supplier if any):
[paste rows]
TASK: 1) Group suppliers by area (nearby, regional, far/online). 2) Draw a simple text map: my business in the middle, suppliers around it, with arrows. 3) Point out any shared dependency (two suppliers relying on the same source, road or distributor). 4) Rate each link LOW / MEDIUM / HIGH concern in plain words.
FORMAT: 1) A text diagram using plain characters (like -->). 2) A table: Supplier | Supplies | Area | Depends on | Backup? | Concern.
RULES: Use only my data. Mark anything unknown as "unknown", don't guess. Don't name any business I didn't give you.
```

**Workflow**
1. Start from your supplier list ([use case 1](02-sourcing-and-suppliers.md)) and dependence check (use case 16).
2. Ask each key supplier, "Where do you get this from?" Write down what they say.
3. Run the prompt.
4. Redraw the map by hand or in a spreadsheet if it helps. Paper is fine.
5. Mark any shared dependency in red, and add it to your playbook (use case 17).

**Worked example (fictional):**
```
   [Grower 1, nearby] --produce-->  \
   [Grower 2, nearby] --produce-->   >  [Farm stand]  <--clamshells-- [Online seller, far]
   [Egg neighbors, nearby] --eggs--> /
   Shared: Grower 1 and Grower 2 both use the same cold-storage co-op (unknown backup) -> MEDIUM
```
The owner sees that the clamshells (packaging) come from one far-away online seller with no backup, rated **HIGH**, and the two growers share one cold-storage spot, rated **MEDIUM**.

**Check the output:** the map is only as good as what suppliers tell you. The AI can't look up who your suppliers really depend on, and any "shared dependency" it suggests without your data is a guess.

---

Back to [overview](01-overview-and-guardrails.md) · Sources: [sources and claims to verify](sources.md)

---

Back to [README](README.md)

Rashon Alsberry, independent portfolio project - [starboy1968.github.io](https://starboy1968.github.io)
