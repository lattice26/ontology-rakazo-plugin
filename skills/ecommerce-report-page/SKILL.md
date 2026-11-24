---
name: ecommerce-report-page
description: Turn e-commerce data agent results into a page (dashboard or report) with metrics, trend charts, rankings and tables, and keep it up to date with a routine. Use for shop diagnoses, daily or weekly business reports, rankings, trends over many days, or when the user asks for a page, dashboard, report or chart of their shop data.
---

# Build a page from the data agent's results

## Where the numbers come from

Build only from what `wait_ontology_agent` returned in this conversation:

- `figures.totals`: headline numbers (`name`, `sum`, `unit`).
- `figures.charts`: daily series. `x` is the dates, each `series` has a `name` and `values` in the same
  order; `null` is a missing day (leave a gap, ⛔ zero).
- `figures.tables`: complete rankings (`columns` with units, `rows`).
- The data sheet's text for anything else, and for the Basis and gaps.

`figures` is everything the agent fetched, labelled by shop (`about`) and dates. The data sheet decides
what counts: use a figure only for a shop and period the sheet reports, and when the sheet says it left
something out (a demo copy of a shop, a revoked shop, a window it replaced), leave it out of the page too.
When a figure and the sheet disagree, follow the sheet.

Copy values as given. Format them for reading ("$184.27", "3 orders") but ⛔ recompute, round further,
fill in or invent a number, label or date. When a section has no data, leave it out.

## Layout (call `save_page` with `{"help": true}` once for the component guide)

1. `Page` titled with the shop and period, e.g. "PetPhone · Nov 15–21". Width "wide" for a dashboard.
2. `Callout` with the conclusion (lead + tone: `warning` when something dropped, `success` when it grew).
3. `Metrics` from `figures.totals`, each with its unit and period.
4. A `Section` per chart: `LineChart` for a daily series (`points` from `x` and `values`, extra series
   as `lines`), the unit in the heading or caption. Amounts and counts on separate charts.
5. `Bars` for a ranking (label column and its value), at most 15 bars, in the order given.
6. `Table` for detail rows, `sortable`.
7. A final `Section` "Basis and gaps" with the sheet's caveats as a `BulletList`, and a `Footnote`
   with the data cutoff ("data complete through 2026-11-21").

For a diagnosis, one `Section` per angle the agent covered (trend, products, creators, refunds, ads),
each with its finding as a short `Text` above its chart or table.

## Keeping it current

When the user wants it daily or weekly ("send me this every morning"):

1. Create a routine on that schedule whose instruction is the same question in the user's words with
   its relative dates ("PetPhone yesterday's GMV, orders, visitors and top 5 products"), and says to
   update this page (its `pageId`) and post a one-line summary with the page link.
2. Each run asks the data agent afresh: ⛔ reuse an earlier run's numbers.
3. Keep the same layout; replace the data, the conclusion and the cutoff date.

Pages start private. Offer to share one only when the user asks to send it to someone.
