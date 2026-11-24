---
name: ecommerce-data
description: Answer questions about the user's e-commerce business with real data — shop sales, GMV, orders, traffic, conversion, products, creators and affiliates, videos and LIVE, ads, refunds and service score, settlements and payouts, category markets and competitors, and brand visibility in AI search (GEO), on TikTok Shop, Shopify or Amazon. Use whenever the answer depends on numbers from these sources, and before saying such data is unavailable.
---

# Ask the e-commerce data agent

A data agent with the user's real shop data answers these questions. It drafts its own plan, queries,
checks definitions and hands back a data sheet. Your job is to pass it the right question, then turn
its sheet into an answer for the user (see the `ecommerce-data-results` skill).

## The call

1. Call `ask_ontology_agent` with the question, then `wait_ontology_agent` with its `turn_id` right away.
   The wait blocks until the answer is ready; if it says the turn is still running, wait again with the
   same `turn_id`. The card under the first call shows the user every step live: do not narrate steps.
2. Pass the `conversation_id` from the first call on every later question in this chat. The agent then
   remembers what it already fetched, which shop was meant and what was decided.
   Start without it only when the user turns to an unrelated shop or topic.
3. If the agent needs the user to decide (which shop, which period), the user usually gets a question
   card while you wait and the wait continues by itself: do not ask again. Only when the wait returns
   `needs_user`, ask the user yourself, then call `reply_ontology_agent` with their answer and wait.
4. If the user changes their mind while it runs, call `cancel_ontology_agent`.

## Writing the question

- **One business question, in the user's words.** "Give my PetPhone shop a deep diagnosis" is one
  question: the agent splits it into the angles it needs (trend, products, creators, refunds, ads…).
  ⛔ Pre-split it into many small asks, and ⛔ ask for things the user did not ask about.
- **Follow-ups say only what changed**: "same, but for last month", "split that by channel",
  "why did the 18th drop?". The conversation already holds the rest.
- **Copy names exactly**: shop names, `@handles`, product titles and ids character for character,
  punctuation included. "PetPhone" and "Pet-Phone" can be two different shops.
- **Tag a bare id with its kind**: `Shop:1784602265804`, `Product:1732504848157741067`,
  `Creator:…`, `Video:…`. A bare long number could be any of them.
- **Keep dates as said**: "yesterday", "last 7 days", "this month". The agent reads them on the
  shop's own calendar. ⛔ Turn them into dates yourself.
- **Keep business words exact**: 样品单 / 寄样单 are sample orders (free samples shipped), not sample
  requests; 退款 is refunds, 退货 is returns; GMV, units sold and orders are different numbers.
- **Remembered defaults**: when the user has told you their main shop or currency, keep it in memory
  and say it in the question ("for PetPhone (TikTok Shop)") instead of making the agent ask again.

## What it can answer

- **The user's own shops** (their own ledger): sales, GMV, orders, visitors, conversion, products,
  affiliate creators, videos and LIVE, refunds and returns, service score, settlements and payouts, ads.
- **The public market**: category sizes and trends, competing shops and products, creators to work with.
- **GEO**: how a brand shows up in AI search answers.

The shop's own ledger and public market figures are two different sets of numbers. A question that
mixes them gets both, labelled; ⛔ compare them as if they were one.
