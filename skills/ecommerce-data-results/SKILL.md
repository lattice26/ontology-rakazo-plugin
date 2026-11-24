---
name: ecommerce-data-results
description: How to read what the e-commerce data agent returns (its data sheet, figures, gaps, needs_user, unavailable and failed outcomes) and turn it into an answer for the user. Use every time wait_ontology_agent returns.
---

# Read the data agent's results

## What comes back

`wait_ontology_agent` returns an `outcome`:

- **answered**: the text is a data sheet. The structured result's `figures` holds the same numbers
  ready for charts: `totals`, `charts` (daily series: `x` dates and `series[].values`) and `tables`
  (complete rankings only; `columns` are plain heading strings). Read the sheet for meaning, use `figures` when you draw or build a page.
- **needs_user**: only the user can settle something (see the `ecommerce-data` skill).
- **unavailable**: it cannot answer this. `reason` says why: `question_unclear` (rephrase or ask the
  user), `data_missing` (the data is not there for that shop or period), `capability_missing` (this
  kind of question is not supported yet), `not_authorized` (the user cannot see that shop),
  `tool_error` (the data service failed; trying again later may work). Tell the user plainly and offer
  its suggestions. ⛔ Fill the gap with estimates or general knowledge.
- **failed**: the turn broke (timeout, service error). Say so and offer to try again; ⛔ guess the answer.

## Reading the data sheet

A sheet has the figures, then a **Basis and gaps** part. Both matter:

- **Every number keeps its period, unit and currency.** Amazon marketplaces each use their own currency.
- **Gaps are part of the answer.** When the sheet says the data stops on an earlier day ("complete
  through 11-21"), that a window moved ("asked for the last 7 days, fetched 11-15 to 11-21"), that a day is
  still collecting, or that an order status is not confirmed, tell the user in one short line next to
  the number it affects.
- **Missing is not zero.** A day without data is unknown. ⛔ Read it as zero, ⛔ fill it in, ⛔ split a
  weekly or monthly total into days.
- **Same shop, counted once.** When the sheet says two shop names are the same store, or one is a demo
  copy, follow it.
- **Own ledger vs market.** Say which one a figure comes from when you put them side by side.

## Writing the answer

1. Lead with the conclusion in one or two sentences: what the numbers mean for the user's question.
   When they asked for a judgement or a recommendation, give it, tied to the figures behind it.
2. Then the evidence: the key figures, a short table when there are several rows. Copy every figure
   exactly as given. When the answer needs a figure the sheet does not have (a share, a growth rate, a
   ratio, a comparison or ranking across results), ask the agent for it in the same conversation first
   (the `ecommerce-data` skill); ⛔ compute it yourself.
3. Then the gaps that change how far the figures can be trusted.
4. End with two or three follow-up directions the user can pick, matched to the question, for example:
   - after a shop diagnosis: which product caused the drop, refund reasons, which creators to keep;
   - after a trend: break it down by channel or product, compare with last period;
   - after a ranking: the trend of the top item, why the bottom ones stalled.
   Offer them; ⛔ run them all yourself.
5. When the answer has a trend, a ranking or several sections, offer to turn it into a page
   (the `ecommerce-report-page` skill). For a full diagnosis or a recurring report, build it.

Where cards do not show (a chat app such as Feishu, Slack or WhatsApp), your text is all the user sees:
make it stand on its own, and link the page if you built one.
